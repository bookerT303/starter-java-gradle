# Getting Started

This guide will use `start.spring.io` to create a zip with the project
files as a maven project structure and provide the steps to
convert to a mono-repo (AppContinuum style)

Start as a monolith and figure out the contexts, features.

There is a pattern that will guide extracting
a microservice from the monolith and create a new application.

## Creating a new project

1. Fork this repository into your new project.

1. `git clone <github url for the forked project>`

1. Use `start.spring.io` to create a zip with the project files using gradle.
    
    Pick the technologies needed for this project.
    
    This is easiest using a web browser to download a zip and then extract
    all the files to you forked project.

1. `./gradlew clean build`

    Make sure it builds before starting to move files and rebuilding
    the gradle files.
    
1. `mkdir -p applications/<app name> components databases docs integration_test`

1. Copy the `build.gradle` to `applications/<app name>`

1. Copy the `build.gradle` to `applications`

1. Add `include "applications:<app name>"` to the `settings.gradle`

1. Move the `src` folder to the `applications/<app name>` folder.

1. Edit the `build.gradle` and leave only the following:
    ```groovy
    plugins {
       id 'io.spring.dependency-management' version '1.0.9.RELEASE'
    }
        
    repositories {
        mavenCentral()
    }
    ```
    
    Add:
    ```groovy
    defaultTasks("clean", "build")
    ```

1. Edit the `applications/build.gradle` and leave only the following:
    ```groovy
    plugins {
        id 'org.springframework.boot' version '2.2.4.RELEASE'
    }
    
    repositories {
        mavenCentral()
    }
    ```
    
1. Edit the `applications/<app name>/build.gradle`
    
    Change the `plugins` into `apply plugin`:
    ```groovy
    apply plugin: 'io.spring.dependency-management'
    apply plugin: 'org.springframework.boot'
    apply plugin: 'java'
    ```
    
1. Make sure the project still builds
