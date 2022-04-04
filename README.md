# qa-backend-challenge

## Welcome
Congratulations! You have reached the technical part for qa backend challenge at ***Doodle***.</br>
Please, ***read carefully*** the instructions on how to set up test environment! Happy bug hunting! 🐞

## How to run
To run system under test in virtualized environment, you have to have ***[Docker service](https://www.docker.com/products/docker-desktop/)*** running on your machine.</br>
The system contains ***backend service***, and it's respective ***PostgreSQL DB***.</br>
Following lines inside `docker-compose.yaml` define resources given by your host machine to the docker containers:
```yaml
    deploy:
      resources:
        limits:
          cpus: '1'
          memory: 2048M
```
You can change here the resources for both service and database according to your needs, but it's tested with this configuration.
</br>
Execute following command in terminal to start the services:
`
docker-compose up
`
</br>
To stop the containers run:
`
docker-compose down
`
</br>
The system is ready for testing once you see message like this in the logs:
```shell
Started BackendChallengeApplication in 3.921 seconds (JVM running for 4.308)
```

## Useful information
Once the application has started API documentation required for testing can be found here: ***[Swagger documentation](http://localhost:8080/swagger-ui.html)***

The system has 4 endpoints:
- */users*
- */slots*
- */meetings*
- */calendars*

The purpose of the service is to manage the meeting scheduling. We can create *Users*, *Slots* and *Meetings*. User is defined
with a name. Slot is defined with startAt and endAt timestamps. Meeting is defined with title, slotId, and participants.

Users are the clients of the platform. Slots represent a time span that can be selected to book a meeting. Why not
booking a meeting directly? Well, we want to decide when meeting can be booked. Meetings represent occupied slots. So
once slot is selected, it becomes a meeting.

These 3 entities are simple one and has basic ***CRD*** operations (no update). For example:
- `POST /users {"name":"User Name"}` will create a user.
- `GET /users/<UUID>` will read specified user.
- `Delete /users/<UUID>` will delete specified user.

Similar applies to all others resources, except Calendar.

Calendar is a bit of specific entity. It contains all the slots and meeting data for the specified month as well as the
count of slots and meetings before and after the selected month. For example:</br>
`GET /calendars/month=2021-03` will return the data for March 2021.

## What we expect:
Given the above information, think of how you would write ***API/Performance*** tests for the test system.</br>
Create the test repository on GitHub(or any other VCS) with instructions on how to run it with your findings and test results.