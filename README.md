Welcome to the assignment! In this assignment, we will try to build a simple chatbot for a restaurant.
We will be using the Rasa framework for this assignment. Do not worry if you have no experience in ML or in using Rasa. All that is required for this assignment can be gleaned from the Rasa tutorial or Rasa docs. 

This assignment is intended to test your learning ability and problem-solving skills together with basic coding skills.

Maximum time required: 3 days

We hope that you have fun learning a new framework and building the chatbot!

# Objective - 
To build a simple chatbot for a restaurant.
The chatbot should be able to the following basic functionalities
- Make a Reservation
- Handle FAQs

Example flows for these functionalities are described in detail in the Flows section.

# Installation

`python 3.6.8` is recommended for use with Rasa!

We highly recommend that you use a fresh virtual environment with python 3.6.8

Rasa 2.0 is the only requirement for this project. Please follow the Rasa installation instructions listed at [https://rasa.com/docs/rasa/user-guide/installation/](https://rasa.com/docs/rasa/user-guide/installation/)

# Instructions

We suggest that you use the [Rasa framework](https://rasa.com/) to build this bot. Rasa is an open-source bot-building platform that will enable you to easily implement the functionalities required for this project.

You can check out this simple [Rasa tutorial](https://rasa.com/docs/rasa/user-guide/rasa-tutorial/) to get an idea of how to approach the problem.

# Flows

Please note that the flows below are only meant as examples to demonstrate functionalities. We would expect the bot to also handle questions having the same meaning but posed in different ways.

## Book Reservation

### Sample Flows

**Flow 1: Booking an AC room at an allowed time**

<ins>Step 1</ins>

User: I want to reserve a table

Bot: How many seats would you like to reserve

<ins>Step 2</ins>

User: 2 seats

Bot: Which section would you like to book
- AC
- Non-AC

<ins>Step 3</ins>

User: (Clicks on Button 1)

Bot: When would you like to book a reservation? (We are only open from 7pm to 10pm)

<ins>Step 4</ins> (Assuminig conversation time is 7:10pm)

User: In half an hour

Bot: You have reserved 2 seats in our AC section for 7:30pm. Thanks!

---

**Flow 2: Booking a Non-AC room at a disallowed time**

<ins>Step 1+2</ins>

User: I want to reserve a table for a party of 4

Bot: Which section would you like to book
- AC
- Non-AC

<ins>Step 3</ins>

User: (Clicks on Button 2)

Bot: When would you like to book a reservation? (We are only open from 7pm to 10pm)

<ins>Step 4</ins> (Assuminig conversation time is 5pm)

User: In half an hour

Bot: We are not open at that time. We are only open from 7pm to 10pm

Bot: When would you like to book a reservation? (We are only open from 7pm to 10pm)

User: 7:30 pm

Bot: You have reserved 4 seats in our Non-AC section for 7:30pm. Thanks!


### Explanation

The system needs the **number of seats**, **section** and **time** from the user to book a reservation.

Flow 1

In step 1, the user only expresses an intent to reserve a table, without providing any additional information. Hence, the bot goes on to ask the three required pieces of information from the user in steps 2, 3 and 4. In step 2, it extracts the required number of seats (2) from the given user inputs (2 seats). In step 4, it extracts the reservation time (7:10pm + 30 mins -> 7:30pm slot) based on the relative time input by the user ('In half an hour'). For understanding why the bot outputs 7:30 pm instead of 7:40 pm, please refer to the specification section.
The flow ends with the bot summarizing the details of the reservation.

Flow 2

In step 1, the user expresses the intent to reserve a table as well as the number of seats. The bot detects the intent as well as extracts the number of seats (4) from the user input. Hence, the bot directly skips to asking the next required information - the section. In step 4, when the user asks to boot the slot ni half an hour, the bot computes the time to be 5 pm + 30 mins = 5:30 pm. Since the restaurant is not open at this time, the bot responds accordingly and repeats the previous question. When the user inputs an acceptable time (7:30 pm), the bot proceeds with the booking.
The flow ends with the bot summarizing the details of the reservation

### Specification

Inputs required for booking
* number of seats: integer / text. Eg. 2, two
* section: button click / text. Eg. Clicking on AC button, AC (in text form)
* time: relative / absolute time. Eg. 7pm, 7:30 pm, In half an hour

The above inputs can be provided by the user step by step or even in the initial request itself. Eg. I want to book 3 AC rooms at 7:30pm. Only the inputs not provided by the user in the initial request should be asked via prompts from the bot.

The restaurant accepts reservations for 30 minutue intervals between 7pm to 10pm each day. Hence, a reservation can be booked for 7pm, 7:30pm, 8pm, ..., 9:30pm. Any times occuring between these intervals should be rounded down. Eg. a request for a reservation at 7:50pm should be booked at 7:30pm.

After accepting all inputs from the user, the bot should summarize the booking information

## FAQs
```
User: What are your timings?
Bot: The restaurant opens at 7pm and closes at 10pm.

User: What days are you open?
Bot: The restaurant is open each and every day.

User: How do I cancel a reservation?
Bot: To cancel a reservation, simply call us at +91 9876543210 and cancel your reservation

User: What are the specials?
Bot: Our chef is a master of the Italian cuisine. Our core speciality is our pasta, which is renowned throughout the city.
```

## Bonus Section
In natural conversations, users do not always follow pre-defined paths. In an attempt to add some flexibility for that, we can add some functionality to handle questions asked in the middle of a pre-defined flow.

For the bonus section, add support to ask any number of FAQs in the middle of pre-defined flows.

**Sample Flow**

User: I want to reserve a table for 4

Bot: Which section would you like to book

- AC
- Non-AC

User: (Clicks on Button 1)

Bot: When would you like to book a reservation? (We are only open from 7pm to 10pm)

User: Are you open today?

Bot: The restaurant is open each and every day.

Bot: When would you like to book a reservation? (We are only open from 7pm to 10pm)

User: At 8pm

Bot: You have reserved 4 seats in our AC section for 8pm. Thanks!

---
Usage of git to iteratively build your code will be much appreciated. It will help us get a good idea about your progress.

## Submission

Please fill out the google form provided in the assignment email to submit your assignment. (It contains some info about your assignment such as link to your repo and model which will help us in auto-grading)

Points to note -

* Make sure that the link to your assignment repo is correct
* Make sure that the responses are *exactly* the same as the bot responses provided in this README
* Make sure that the link to your model is visible and downloadable
* Your model should be a google drive link of the form https://drive.google.com/file/d/<file_id>/view?usp=sharing

**All of these are essential for us to auto-grade your submission.**

Hope that this would be a fun experience for you and you learn something interesting. Happy coding!

Humble request 🙏 - Do not make your assignment repo public after you are done with the assignment
