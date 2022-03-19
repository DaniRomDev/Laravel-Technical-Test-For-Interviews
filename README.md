# Table of contents

- [Table of contents](#table-of-contents)
- [Docker environment documentation](#docker-environment-documentation)
- [Before you begin to code](#before-you-begin-to-code)
  - [Detail explanation](#detail-explanation)
  - [Pair programming session](#pair-programming-session)
- [Booking system for electric cars by subscription](#booking-system-for-electric-cars-by-subscription)
  - [Critical business logic:](#critical-business-logic)
  - [User stories](#user-stories)
    - [Available electric cars list](#available-electric-cars-list)
    - [Detail electric car](#detail-electric-car)
  - [Subscribe to an electric car](#subscribe-to-an-electric-car)

# Docker environment documentation

All the documentation to get up and running with the prepared docker environment is on [Docker starter PHP](https://github.com/DaniRomDev/Docker-Starter-PHP/blob/main/README.md)

**Important note:** This is an optional step and you can use the development environment for Laravel projects that you feel more comfortable working with. We simply provide a good environment compatible with several operating systems in which you will only need to have Docker installed on your main machine and run a simple `make` command in the root of the project.

# Before you begin to code

Be aware that **_you don't need to finish all the users stories_**, the main objective is to see how organized you are when creating the code, the git commits, if you apply clean code concepts, test suites for your new code, etc.

We prefer that you finish one user story but fully tested and well organized that all of them but without any test or not having in mind if another developer is going to read your code in the future (or you).

## Detail explanation

- Work on the project. You can take as long as you feel you need, however, we urge you not to spend more than a few hours. **_Remember: we are evaluating how well you would fit on a team of developers, not working in isolation._**
- Once you have finished your work please **tag your development branch as** **_1.0_** and reply to the email that invited you to do the project to let us know it is complete.

## Pair programming session

Please use this as an opportunity to show us how good you are at coding and not how quick, we are interested in quality, not quantity, in the context of a team of developers.

Once you've finished **_we will organise a pair programming session_** where you can explain your code and add some features.

If you have any questions during the project please ask via **Slack**. We will add you to our **Slack** channel shortly and you will receive an invitation. Please use it to to ask any questions and to communicate your progress during the project.

We look forward to hearing from you!

# Booking system for electric cars by subscription

This reservation system allows users to access an electric car in a subscription format _(like Netflix)_, with a minimum subscription duration of one month and a maximum of 12 months. There is a initial payment _(with extra fees and other stuff)_ and recurring payments each month _(only the electric vehicle price)_.

**Note:** Use to your advantage all the tools offered by the framework and the external libraries you need to accomplish the task. Be cautious when deciding if you really need that external library to complete the task.

## Critical business logic:

- The electric car list can be seeing by anyone
- The user needs to be authenticated to be able subscribe a car
- The users can only have one active subscription.
- The monthly price is differente based on the subscription duration _e.g: 3 months - 500 €, 6 months - 435€_
- The electric vehicle under subscription should not be available for other users to subscribe to.
- A new invoice should be created for each payment and send to the user via email in PDF format.
- A subscription is not active until the electric car is delivered to the customer
- The user can cancel the subscription at anytime
- The cancelation begins a collection of the electric car if this one is already delivered

## User stories

### Available electric cars list

**As a customer**
I want to see the list of available electric cars
So that I can see all the available cars and select each to see detailed info

**User Acceptance Criteria:**
GIVEN the electric cars list
WHEN the user selects him
THEN I can see the electric car details

### Detail electric car

**As a customer**
I want to see the electric car detail
So that I can decide if want to subscribe to the electric car

**User Acceptance Criteria:**
GIVEN the electric car unique identifier
WHEN the user wants to see the electric car detail
THEN I can see the electric car detail and be able to start a subscription process

## Subscribe to an electric car

**As a customer**
I want to see the summary of my subscription
So that I can do the initial payment

**User Acceptance Criteria:**
GIVEN the electric car and subscription summary
WHEN the user wants to pay for subscription
THEN I can subscribe to the electric car selected
