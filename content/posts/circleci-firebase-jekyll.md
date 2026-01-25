+++
title = 'How to Deploy a Jekyll Site to Google Firebase with CircleCI'
date = 2023-09-19T14:00:00-07:00
categories = ['dev', 'ci', 'blog']
author = 'Colin'
+++

After building this site I wanted to set it up to automatically publish when I committed my code. I found some instructions for [Travis](https://www.travis-ci.com/), but the fee on that is way too high for a small personal site like this one. Looking around some more, it seemed that [CircleCI](https://circleci.com/) would be good as it has a free plan that works for something used as infrequently as a blog. Unfortunately, there weren't any good tutorials on how to set up CircleCI for a Jekyll site deploying to a [Firebase](https://firebase.google.com/) static page host. So, here's the instructions I wish I had yesterday.

## 1 Make a CircleCI Account
This should be obvious but the first thing you need to do is make an account on [CircleCI](https://circleci.com/) and link it to [GitHub](https://www.github.com). I wouldn't bother setting up any projects yet, we can do that after we've created the config.

## 2 Make the config.yml
Like Travis, CircleCI works by setting up a [yaml](https://yaml.org/) config file that Circle will read every time you commit code to your repository. It uses it as a set of instructions to run on a remote machine to do whatever your build is. For our purposes, we need a config that will set up Jekyll and Firebase, build our site, then publish it to firebase. We'll need access to [NodeJS](https://nodejs.org/en) for the Firebase install, and [Ruby](https://www.ruby-lang.org/en/) for Jekyll. Finally, we'll need to set up an API key for CircleCI to publish the site to Firebase as we can't interactively login like we normally would.

You can find my [current config](https://github.com/Jearil/aspirations/blob/main/.circleci/config.yml) in the [source](https://github.com/Jearil/aspirations) for this site, but here it is for easy reference. Please note this file is named config.yml and exists in a .circleci directory in your root directory of your project.

```yaml
version: 2.1

workflows:
  build:
    jobs:
      - build

jobs:
  build:

    working_directory: ~/repo

    # docker hub images https://hub.docker.com/
    docker:
      - image: cimg/ruby:3.1.4-node
    resource_class: small

    steps:
      - checkout

      - run:
          name: Ruby dependencies
          command: bundle check || bundle install

      - run:
          name: Build
          command: bundle exec jekyll build --verbose

      - run:
          name: Firebase Setup
          command: npm install firebase-tools --unsafe-perm

      - run:
          name: Deploy Site
          command: ./node_modules/.bin/firebase deploy --token "$FIREBASE_API_TOKEN"
```

I am not an expert on this, but I can tell you a few things. First, CircleCI uses [Docker](https://www.docker.com/) images when spinning up your environment. You can make your own, or use ones they've already provided. They have ones for different common dev environments like ruby or nodejs. It took some digging, but I found that one of the ruby images also includes nodejs as well. We can see that being used here:

```yaml
    docker:
      - image: cimg/ruby:3.1.4-node
```

So now that we have an environment that runs both ruby and node, we need to install our gems which we can do with our `Ruby dependencies` run command. Each of the `run` commands is like typing something on the command line. To set up our environment, build, and deploy we only really need 4 commands:

```bash
$ bundle check || bundle install
$ bundle exec jekyll build --verbose
$ npm install firebase-tools --unsafe-perm
$ ./node_modules/.bin/firebase deploy --token "$FIREBASE_API_TOKEN"
```

Note the Deploy command uses a relative path to the firebase binary as the install was local and not global (no -g option). I found that circleci prevented `-g` for security reasons and this works well enough. Commit the config before heading on to the next step.

There are additional things you can do here like cache some of your config to make it faster, but I haven't learned that yet. I'll update this tutorial once I figure that out.

## Configure CircleCI
Back to [CircleCI](https://circleci.com/), you can now set up your project. In the Projects tab on the left you should get a list of all of your GitHub repos. Select the one you want and Set UP Project. Under Select your config.yml file there should be an option for "Fastest: Use the .circleci/config.yml in my repo. You'll also have to type in your branch, probably `main`. The build will automatically start, and you can see it running by clicking into the build section. It will fail however, because firebase does not have any login information. That's the next part we must set up.

### Setup Environment Variables
In your project go to Project Settings -> Environment Variables. We're going to add 2 variables here, one for setting Jekyll to production, and the other to set the Firebase API Key. First, bring up a terminal and run:

```bash
$ firebase login:ci
```

It will have you login and give you an API key on the terminal. Copy that and paste it into a new environment variable in CircleCI named `FIREBASE_API_TOKEN`. Create a second variable named `JEKYLL_ENV` with a value of `production`.

You should now be able to go back to the project and rerun it. Looking at the output, it should now compile your site and publish it with firebase.

That's all of what I wish I knew yesterday when trying to set this up.
