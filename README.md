# qa-backend-challenge

## Welcome
Congratulations! You have reached the technical part of the QA backend challenge at ***Doodle***.</br>
Please, ***read carefully*** the instructions on how to set up the test environment! Happy bug hunting! 🐞

#### Table of Contents

1. [Setup](#setup)
2. [Useful information about the API](#useful-information-about-the-api)
3. [Task](#task)

## Setup
To run the system under test in a virtualized environment, you have to have ***[Docker service](https://www.docker.com/products/docker-desktop/)*** running on your machine.</br>
The system contains ***backend service***, and its respective ***PostgreSQL DB***.</br>

---
**NOTE**
The following lines inside `docker-compose.yaml` define resources given by your host machine to the Docker containers:
```yaml
    deploy:
      resources:
        limits:
          cpus: '1'
          memory: 2048M
```

Here you can change the resources for both service and database according to your needs, but it's tested with the given configuration.

---

Execute the following command in the terminal to start the services:
`
docker-compose up
`
</br>
To stop the containers run:
`
docker-compose down
`
</br>
The system is ready for testing once you see a message like this in the logs:
```shell
Started BackendChallengeApplication in 3.921 seconds (JVM running for 4.308)
```

## Useful information about the API
Once the application has started API documentation required for testing can be found in the ***[Swagger documentation](http://localhost:8080/swagger-ui.html)***

The system has four endpoints:
- */users*
- */slots*
- */meetings*
- */calendars*

The purpose of the service is to manage the meeting scheduling. We can create: 
- *Users* - represent clients of the platform. User is defined with a `name`. 
- *Slots* - represent a time span that can be selected to book a meeting. Slot is defined with `startAt`, and `endAt` timestamps.
- *Meetings* - represent selected slots. Once a slot is selected, it becomes a meeting. A meeting is defined with a  `title`, `slotId`, and `participants`. 

These three entities are simple and have basic ***CRD*** operations (no update). For example:
- `POST /users {"name":"User Name"}` will create a user.
- `GET /users/<UUID>` will read the specified user.
- `DELETE /users/<UUID>` will delete the specified user.

Similar applies to all other resources, except Calendar which is a bit of a specific entity.

Calendar - contains all the slots and meeting data for the specified month as well as the
count of slots and meetings before and after the selected month. For example:
- `GET /calendars/month=2021-03` will return the data for March 2021.

>TIP: There is already some pre-generated test data populated at the boot time, to help you get started! 

## Task
Given the information above, think of how you would write ***API*** tests for this test system and create test suite accordingly. </br>
Send us a link to the test repository you created on GitHub (or any other VCS) containing instructions on how to run it, including your findings and test results.</br>
>NOTE: If you do not feel comfortable with API tests and would rather create performance tests - that's alright with us, too.</br>