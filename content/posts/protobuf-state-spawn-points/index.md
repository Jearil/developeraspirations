+++
title = 'Rethinking Persistence'
date = 2024-06-09T17:00:00-08:00
categories = ['dev']
tags = ['gamedev']
author = 'Colin'
image = 'title.png'
+++

It's been a while since I've posted and the amount of work I have to show for it is more reflective of the number of posts I've made rather than the amount of time has passed.

So not a lot.

However, I did do 2 major things faily recently. To start, I spent some time actually coming up with the main story of the game. It's mostly broad right now but it does deal with a Glutenmancer and bread products and is a quest of sorts. I'm leaning a lot towards some sort of RPG featuring this glutenmancer. I don't know how much I want to really talk about the story however as it would give away a bunch of the main game and I think at this point I still want this to mainly be a developement blog about the process of building my game. Secondly, I changed how I'm thinking about persistence.

With that in mind, the last time I posted was about [persisting game state]({{< ref "/posts/persisting-state-godot" >}}). That system was very generic and might have been useful for saving state of generic nodes, but it was getting hard to work with. It also felt just more difficult to use than I really wanted. Ideally, I want to not really have to think so much about game saving or loading, just dealing with data. So I wanted to rethink the whole system.

## What is data?

The last time I asked "What is Persistence?" and talked about saving and loading game state. I wanted to back up on this concept though, and think more about the data itself. What is data and how do we get, use, and store data? I'm thinking more of how on a low level I'll want to store any data that any object will use at runtime in the app itself. And there's a few ways of doing that really.

The first thought is that data generally would go with the `Node` or system that uses that data. If we have a Character node, it would have different properties and could store that data as variables that are part of that node. So if your character has a name, you could make a name member variable. The node already has some data that I'll want to store already like a Character's X and Y coordinates in the scene you're currently in, so the node makes sense in a way.

```csharp
public partial class Character : CharacterBody2D
{
    private string Name;
    // Position.X
    // Position.Y

    public override void _Ready()
    {
        // Load Data
    }

    public override void _ExitTree()
    {
        // Save Data
    }
}
```

The problem with this approach is we still have to store and restore the data. We'd need to either save the data in each of our classes or put it into a central location to be saved. Ideally, I'd want the Nodes that are used to do the least amount possible, and that includes not really dealing with their own data. One way of doing this in Godot is to use [Resources](https://docs.godotengine.org/en/stable/tutorials/scripting/resources.html), which honestly is how it should probably be done. Resources can be persisted pretty easily in Godot and restored as well. However, Resources have a [large security flaw](https://github.com/godotengine/godot-proposals/issues/4925) that makes it not ideal to use Resources as a save file format. JSON has typically been used instead, and indeed my first attempt at a persistence layer used JSON as well. However, JSON is frustrating as it only uses basic types and converting the data into custom types is a manual process that involves a lot of casting. I wanted to use a better method that can quickly serialize and deserialize data while retaining type information. This lead me to a system I actually use in my day job at Google.

## Protobufs

There's a fairly generic library for serializing and deserializing data in Google's [Protobufs](https://protobuf.dev/). I'll define all of my data objects as proto files which will auto-generate C# classes. I can then just make data objects using these classes and store them using the classes `ToByteArray()` method. I can restore it using the data classes `Parser.ParseFrom(byteArray)` to restore. Protobufs were designed to be really fast so the data serialization and deserialization should be fast enough to make really quick saving and restoring.

## Game State

Rather than having each `Node` or other class that wants to store and restore data from implementing saving or loading, I instead am going to try using a centralized storage node called the `GameState`. `GameState` is a data object defined as a protobuf that will contain *all* of my game's data. The idea is that I have a `GameStateManager` that will hold this global game state. It either creates a new one on a new game creation, or loads it from disk on game load. When the game is quit or manually saved, we merely serialize the state using `GameState.ToByteArray()`. The `GameStateManager` is [autoloaded](https://docs.godotengine.org/en/stable/tutorials/scripting/singletons_autoload.html) into all Scenes. All nodes grab an associated object from the `GameState`. They use this object to store any of their own state. Since we always use the `GameState` object to store everything we want to save/restore, we don't have to do anything overly special on each node or class other than create a data proto and insert it into the `GameState` somewhere. Currently I have very little in my `GameState`, but this is what it looks like so far:

```protobuf
syntax = "proto3";
import "Proto/CharacterData.proto";
import "Proto/TransitionData.proto";

option csharp_namespace = "BreadQuest.Data";

message GameState {
  CharacterData character = 1;
  TransitionData transition = 2;
}
```

I'll talk about `TransitionData` in a later post, but let's show the `CharacterData`.

```protobuf
syntax = "proto3";

option csharp_namespace = "BreadQuest.Data";

message CharacterData {
  Position position = 1;
}

message Position {
  float X = 1;
  float Y = 2;
}
```

The only thing we're starting with for our character is storing the character position. When we quit the game, we save everything to disk. When we start the game again, we reload from disk. The character class will load it's position if it exists.

```csharp
private CharacterData _characterData;
private GameStateManager _gameStateManager;

public override void _Ready()
{
    _gameStateManager = GetNode<GameStateManager>("/root/GameStateManager");
    InitCharacterData();
}

private void InitCharacterData()
{
    _characterData = _gameStateManager.GameState.Character;
    if (_characterData == null)
    {
        _characterData = new CharacterData();
        _gameStateManager.GameState.Character = _characterData;
        _characterData.Position = new Position();
        _characterData.Position.X = Position.X;
        _characterData.Position.Y = Position.Y;
    }
    else if (_characterData.Position != null && _gameStateManager.GameState.Transition.Id == 0)
    {
        var x = _characterData.Position.X;
        var y = _characterData.Position.Y;
        Position = new Vector2(x, y);
    }
}

public override void _PhysicsProcess(double delta)
{
    // do stuff
    SaveData();
}

private void SaveData()
{
    _characterData.Position.X = Position.X;
    _characterData.Position.Y = Position.Y;
}
```

When my character is created, it checks to see if there's already a data object for it. If there isn't, it creates one. This makes sure we always have a data object. I'm thinking all objects will have to do this in the _Ready() method to create their data. I'm not sure how this will work with Resources that the Node uses as copying between a Resource and a proto might be annoying. I guess I'll cross that bridge when I get there. I may just not use Resources very much, which I'm sure a lot of people would say I shouldn't do. Anyway, this is how I'm going to try for my game.

My character can move around the map which mainly happens in `_PhysicsProcess`. At the end of doing that I store the current position into our `CharacterData`. Normally I would only use data in the `CharacterData`, but Position is a built-in property of `CharacterBody2D` that I'm using and it needs to be synchronized to my data store.

Since the `GameStateManager` auto-saves on exit and auto-loads on startup, my character position will get restored as well. The basic system worked and let me save where the character was.

## Transitions

I did one other thing as I played around with my new persistence system and that was doing transitions between scenes. However, I think I'll write up a separate article for that. This is it for now.
