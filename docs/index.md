# Introduction
This documentation is intended to help you through learning the basics of JavaFX for building a simple game.

For more information about JavaFX please visit the official [JavaFX website](https://openjfx.io/).

## Intended Users
This guide is for term 2 CST students intending to use JavaFX to create their Object Oriented Programming term project. We will cover the general features that most term projects will have.
<!-- We may want to expand on what those features are/ re-word this sentence -->

## Prerequisite Knowledge
To follow this guide you should have:

- Working knowledge of Java - at least what has been covered in your Object Oriented Programming course so far.

- Some knowledge of CSS style sheets - helpful to have, but not required.
## Software Requirements
- Java 11 or later
- IntelliJ IDEA

## Overview

## Formatting (Typographical Conventions)
Code blocks will have a title indicating what class the code is placed in.
<!-- class or file? -->
``` java title="Addition.java" linenums="1"
    public class Addition {
        private int num1;
        private int num2;

        public Addition(final int num1, final int num2){
            this.num1 = num1;
            this.num2 = num2;
        }
    }
```
Any additions to previous code will be highlighted.
``` java title="Addition.java" linenums="1" hl_lines="10-12"
    public class Addition {
        private int num1;
        private int num2;

        public Addition(final int num1, final int num2){
            this.num1 = num1;
            this.num2 = num2;
        }
        
        public int Add(){
            return num1 + num2;
        }
    }
```
## Notes and Warning Messages (Admonitions)
<!-- We may want to change what these contain once we start writing the tasks -->
!!! note
    Notes provide additional information for a step.

!!! success
    Success indicates what a successful result should look like.

!!! warning
    Warnings contain crucial information about steps that may cause errors if done wrong.
