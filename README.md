# Table of contents

- [Table of contents](#table-of-contents)
- [Our review process](#our-review-process)
- [Docker environment documentation (Optional)](#docker-environment-documentation-optional)
    - [Initial setup for Linux/MacOS _(go to the documentation if you are using Windows)_](#initial-setup-for-linuxmacos-go-to-the-documentation-if-you-are-using-windows)
- [Before you begin to code](#before-you-begin-to-code)
  - [Detail explanation](#detail-explanation)
  - [Pair programming session](#pair-programming-session)
- [Booking system for electric cars by subscription](#booking-system-for-electric-cars-by-subscription)
  - [Critical business logic to have in mind:](#critical-business-logic-to-have-in-mind)
  - [Entities](#entities)
    - [User](#user)
    - [Subscription](#subscription)
    - [Electric vehicle](#electric-vehicle)
    - [Invoice](#invoice)
  - [User stories](#user-stories)
    - [Available electric cars list](#available-electric-cars-list)
    - [Filter available electric cars list](#filter-available-electric-cars-list)
    - [Detail electric car](#detail-electric-car)
    - [Subscribe to an electric car](#subscribe-to-an-electric-car)
    - [Update my subscription length](#update-my-subscription-length)
    - [See invoice on user email as an attachment](#see-invoice-on-user-email-as-an-attachment)
    - [See/Download invoices inside the application](#seedownload-invoices-inside-the-application)
    - [Cancel my subscription without electric car delivered yet](#cancel-my-subscription-without-electric-car-delivered-yet)
    - [Cancel my subscription with electric car delivered](#cancel-my-subscription-with-electric-car-delivered)

# Our review process

The technical test is the same for all levels but depending on the job position, the requirements will be different. **None of the positions have to complete all the user stories**

**As a Junior position:** if you know the basic fundamentals of Laravel/PHP and can complete at least 2 user stories with minimal quality is enough _(Unit tests are optional but highly recommended)_

**As a Mid developer position:** if you use some design patterns, have SOLID principles in mind, use the framework to your advantage, have a solid database knowledge with the extra of having a good test suite is enough.

**As a Senior:** Here we will be a bit more demanding and we assume that you know the framework very well and have worked some years with PHP. You think about scalability and maintainability of the code even if the tasks are simple because you know that the application will grow sooner or later. You don't lack tests and you document the necessary parts so that other developers have the right information _(the deploy of the application would be awesome but it's totally optional)_

# Docker environment documentation (Optional)

**Important note:** This is an optional step and you can use the development environment for Laravel projects that you feel more comfortable working with in your host machine. We simply provide a good environment compatible with several operating systems in which you will only need to have Docker installed on your main computer.

While you can work on the **src** folder with a laravel project and upload the code to the repository, is enough for us.

### Initial setup for Linux/MacOS _(go to the documentation if you are using Windows)_

```sh
 cp .env.example .env && make && make install-laravel && make restart
```

All the documentation to get up and running with the prepared docker environment is on [Docker starter PHP](https://github.com/DaniRomDev/Docker-Starter-PHP/blob/main/README.md)

# Before you begin to code

Be aware that **_you don't need to finish all the users stories_**, the main objective is to see how organized you are when creating the code, the git commits, if you apply clean code concepts, test suites for your new code, etc.

We prefer that you finish one or two user stories but fully tested and well organized that all of them but without any test or not having in mind if another developer is going to read your code in the future (or you).

## Detail explanation

- There is no single path to complete a user story, whether you want to create the application as a REST api or a combination of web and REST api is up to you, only be consistent in what you do.
- Work on the project. You can take as long as you feel you need, however, we urge you not to spend more than a few hours. **_Remember: we are evaluating how well you would fit on a team of developers, not working in isolation._**
- Once you have finished your work please **tag your development branch as** **_1.0_** and reply to the email that invited you to do the project to let us know it is complete.

## Pair programming session

Please use this as an opportunity to show us how good you are at coding and not how quick, we are interested in quality, not quantity, in the context of a team of developers.

Once you've finished **_we will organise a pair programming session_** where you can explain your code and add some features.

If you have any questions during the project please ask via **Slack**. We will add you to our **Slack** channel shortly and you will receive an invitation. Please use it to to ask any questions and to communicate your progress during the project.

We look forward to hearing from you!

# Booking system for electric cars by subscription

This reservation system allows users to access an electric car in a subscription format with a minimum subscription duration of 1 month and a maximum of 12 months. There is a initial payment _(with extra fees and other stuff)_ and recurring payments each month _(only the electric vehicle price)_.

**Note:** Use to your advantage all the tools offered by the framework and the external libraries you need to accomplish the task. Be cautious when deciding if you really need that external library to complete the task.

---

## Critical business logic to have in mind:

- The electric car list can be seeing by anyone
- The user needs to be authenticated to be able subscribe an electric car
- The users can only have one active subscription.
- The monthly price is different based on the subscription duration _e.g: 3 months - 500 €, 6 months - 435€_
- The electric vehicle under subscription must not be available for other users to subscribe to.
- A new invoice should be created for each payment and send to the user via email in PDF format.
- A subscription is not active until the electric car is delivered to the customer
- The user can update the subscription length at anytime
- The user can cancel the subscription at anytime
- The cancelation begins a collection of the electric car if this one is already delivered

## Entities

We give you the basic models but feel free to add new properties or create new models if needed. The creation of the models, migrations, database fields, files that you think you need is up to you as long as you can explain it in the pair programming session.

Create the necessary entities of the user stories you are going to complete, if for example you are not going to complete anyone related to invoices, do not create the invoice model.

### User

**Relationships:** Subscriptions, Invoices
The default properties that comes with Laravel are enough

### Subscription

**Relationships:** User, Electric Vehicle, Invoices

- Status _(NEW, ACTIVE, DELIVERY_PROCESSING, COLLECTION_PROCESSING, CANCELLED, ENDED)_
- Starts at
- Ends at
- Cancelled at
- Cancellation reason
- Monthly price
- Electric car delivery date
- Electric car collection date

### Electric vehicle

**Relationships:** Subscription

- Make
- Model
- Battery size
- Registration plate
- Status (AVAILABLE, ON_DELIVERY, UNDER SUBSCRIPTION, ON_COLLECTION, NOT AVAILABLE)
- Price
- Price variations _(only for 3, 6, 9 , 12 months subscriptions)_
- Real word range _(in miles)_
- Max speed _(in miles/hour)_

### Invoice

**Relationships:** User, Subscription

- Type _(Initial Payment, Monthly Payment)_
- Total
- Description
- Payment date

## User stories

### Available electric cars list

**As a user**
I want to see the list of available electric cars
So that I can see all the available cars and select each one to go to a detail view

**User Acceptance Criteria:**
GIVEN the electric cars list
WHEN the user select one of them
THEN I can see the electric car details

### Filter available electric cars list

**As a user**
I want to filter _(including sort)_ the list of available electric cars by price, real world range, battery size, max speed
So that I can see all the available cars and select each one to go to a detail view

**User Acceptance Criteria:**
GIVEN the electric cars list
WHEN the user apply or remove a filter
THEN I can see the electric car list filtered by selected filters

### Detail electric car

**As a user**
I want to see the electric car detail
So that I can decide if I want to subscribe to the electric car

**User Acceptance Criteria:**
GIVEN the electric car unique identifier
WHEN the user wants to see the electric car detail
THEN I can see the electric car detail and be able to start a subscription process

### Subscribe to an electric car

**As an authenticated user**
I want to subscribe for the selected car
So that I can do the initial payment to complete subscription

**User Acceptance Criteria:**
GIVEN the electric car and subscription length
WHEN the user wants to pay for subscription in electric car detail
THEN I can subscribe to the electric car selected

### Update my subscription length

**As an authenticated user**
I want to change my subscription length
So that I can see the subscription monthly price and end date updated

**User Acceptance Criteria:**
GIVEN the user subscription and the new length
WHEN the user update the subscription
THEN I can see my subscription monthly price and end date updated

### See invoice on user email as an attachment

**As a registered user**
I want to see the invoice in PDF format on my email
So that I can have information about my subscription payments

**User Acceptance Criteria:**
GIVEN the user subscription
WHEN a new payment was charged to the user
THEN I can receive an email with the new invoice

### See/Download invoices inside the application

**As a registered user**
I want to see my invoices in the application
So that I can have information about my subscription invoices and download them

**User Acceptance Criteria:**
GIVEN the authenticated user
WHEN I would like to see a list of my invoices
THEN I can see the list of my invoices and download in PDF format

### Cancel my subscription without electric car delivered yet

**As a registered user**
I want to be able to cancel my subscription at anytime
So that I can stop using the electric car and be able to subscribe to a new vehicle

**User Acceptance Criteria:**
GIVEN the authenticated user and the subscription
WHEN I request to cancell my actual subscription
THEN I can see an email notification with my subscription cancelled and my initial payment refunded

### Cancel my subscription with electric car delivered

**As a registered user**
I want to be able to cancel my subscription at anytime
So that I can stop using the electric car and be able to subscribe to a new vehicle

**User Acceptance Criteria:**
GIVEN the authenticated user and the subscription
WHEN I request to cancel my actual subscription
THEN I can see an email notification with my subscription cancelled and the information of the collection in process for my electric car that's going to be done 1 week after the cancellation request day.
