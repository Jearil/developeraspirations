+++
title = 'Learning Rust'
date = 2025-01-21T20:00:00-08:00
categories = ['dev']
tags = ['programming']
author = 'Colin'
+++

I used to attempt to learn a new langauge (programming) every year. I fell out of the habit around 2011 or so, and to an extent I lament that. I learned Ruby, JavaScript, Scala, Python, and a few others just to get a feel for those languages. I ended up using Scala and Python in a work environment, but most of the time it was just to think differently about my main programming languages. It also kept me interested and excited for programming.

Part of doing game development for me (which has stalled, but I'll get back to it), has been learning the new environments and languages. I've played with C# in the past, but not to any great extent. Using Godot, I get to practice C# a lot more and learn more of that. I use Protocol Buffers every day at work, but a lot of it is already set up and generating. Starting from scratch was a great thing to better understand how that works as well. I wanted to start learninga gain to gain more passion for programming so I decided to take a course offered by my job. That course is [Comprehensive Rust](https://google.github.io/comprehensive-rust/).

I'd like to share just a few of my learnings and take-aways from that experience.

A lot of people have written a lot of things about Rust. It's a hot new(ish) language that's becoming really popular and exciting right now due to it's more safe nature than C/C++. I don't have a lot of experience in Rust. Mainly just the course I took. I'm not writing this to convince anyone to try or use Rust. I've hardly used it enough myself to really make that judgement. However, I have written a lot of Java code in my life. And I at least have that perspective. This is not going to teach you Rust or even tell you that you should use it. It's just a perception of the language by someone who's traditionally used Java based languages for 20 years.

# Structs are Objects

Though I primarily use Java, I have learned enough of C to know what a struct is. From my understanding, it was always just a block of data. Useful, but somewhat limited in application in Object Oriented Programming. In Java we have classes. In Kotlin there are data classes. Rust doesn't have classes, just structs. So at first it seeemed like it would be more like a pure functional language. However, Rust has a way of associating functions with structs. This gives us methods and makes structs sort of act like a Java class.

```rust
struct Person {
    name: String,
    age: i32,
}

impl Person {

    fn new(name: &str, age: i32) -> Self {
        Self { name: String::from(name), age: age }
    }

    fn print(&self) {
        println!("Hi, I'm {} and I'm {} years old", self.name, self.age);
    }
}

fn main() {
    let colin = Person::new("Colin", 42);
    colin.print();
}
```

In this way, the `Person` struct acts in a way like a class. It has a `new` method to create new instances of it. There's also a print method to print out some of the details of the struct. These methods are associated with the `Person` struct within an `impl` block. However, you'll notice that each of the methods takes in a reference to self as the first arguement. In a way, I think of these struct methods really as just normal functions that take in a particular struct as the first arguement.

It makes me think about how to add object oriented design to a purely functional language through the use of static methods that akways take a data structure as the first arguement. There is then the syntatical sugar of using the variable of that struct and either dot notation or colon notation to call methods that implicitly pass the struct in as the first variable of the function. It's pretty elegant. And it works quite well with the next feature of Rust that I enjoyed.

# Traits
Traits were familiar to me if I thought about them as interfaces. And in a way, they are a lot like interfaces. You can define methods on a trait and implement them in association with a struct to give it behavior. However, traits also act as a way to extend a "class" by assigning new methods to existing structs. You can't just add additional methods onto a struct if an `impl` already exists, but you can create a new trait and have an implementation of that trait in association with a struct. This lets you extend it which is pretty handy.

If we take the above code and want to add new behavior as a user of the library that includes the `Person` struct, we can do so in the following way as a trait.

```rust
trait Programmer {
    fn code(&self);
}

impl Programmer for Person {
    fn code(&self) {
        println!("{} has been programming for {} years", self.name, self.age);
    }
}

fn main() {
    let colin = Person::new("Colin", 42);
    colin.code();
}
```

In this way, we added in a `code` method to the `Person` struct in addition to its existing `print` method. For me, this gives Rust more tools for doing object oriented programming in a more functional way.

# Enums

Enums are huge in Rust. One of my favorite things about the language is that the language does not have exceptions. I've found exceptions to be inelegant and one of my least favorite things about languages like Java (and a lot of other languages). Exceptions, break the control flow in weird ways that are often not handled and just left dangling. It can result in crashes, or be "handled" by being caught and ignored.

Why do I talk about this in relation to the enum data structure? The enum in Rust honestly acts mostly like what you'd expect (though a lot more powerful). It's a somewhat hard set list of values that one can match upon. And matching is really powerful in Rust. Moreso, the way that Rust handles not having exceptions is that for any method that could fail, instead of returning a normal result, it returns an Enum that either contains the result or an error.

In Java, an Enum can contain a value. And it can in Rust too.

```rust
enum Result<T, E> {
    Ok(T),
    Err(E)
}

fn divide(i32 num, i32 denom) -> Result<i32, String> {
    if (denom == 0) {
        Err(String::from("Cannot divide by 0"))
    }
    return num / denom;
}

fn main() {
    val result = divide(3, 0);
    val toPrint = match result {
        Ok(number) => format!("Your result was {number}"),
        Err(error) => error
    }
    println!(toPrint);
}
```

The error had to be handled as what's returned isn't just the result, it's either a result or the error. Expand this idea to any method. If you try to open a file, it returns an `enum` of either the file or an error which you now have to handle. There's also a few things to make handling these errors less tedious through the use of the `?` operator to propegate errors and assume that the result didn't have an error. If there was an error, it returns the error early, otherwise it continues with the flow.

# Other things

The course I took was only 4 days over 2 week so I feel like it really only gave me a taste of the language. I didn't really get much into `async` I only briefly touched upon smart pointers. There's also unsafe Rust which I understand as a necessity for interop, even if I don't generally like the idea in the language itself.

I don't know if I'll get much of a chance to program in Rust myself. There are [bindings for Godot](https://godot-rust.github.io/), but I'm still just learning the engine and sticking with C# is probaly the best for that. If I can think of any projects though, I totally want to play with it. I was thinking of maybe making some windows programs, but I haven't done much with Windows programming and the APIs for it that I looked up look really old and obtuse (I'm not a C/C++ windows programmer). Maybe if I find a different GUI framework that I'm ok with I can do some personal projects.

Or if anyone has some suggestions, leave a comment below.
