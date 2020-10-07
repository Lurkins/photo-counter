# Photo Counter

A simple photo rating app built with Vue.js, Flask, Mongodb, all running in Docker containers. 

## Getting Started

Clone the repo to your local machine and launch in Docker. See below for details.

### Prerequisites

You will need Docker installed on your system to run the app. You can download and install Docker from https://www.docker.com/

### Installing

From terminal, clone the repositiory.

```
git clone https://github.com/Lurkins/photo-counter.git
```

Change directories into the project.

```
cd photo-counter
```

Run the app with Docker compose. Installation may take some time.

```
docker-compose up
```

Once Docker has built and run all the containers visit http://localhost:8080/ in a browser.

Upload your images and rate them with the +1 / -1 buttons.

## Built With

* [Vue](https://vuejs.org/) - Frontend UI
* [Flask](https://palletsprojects.com/p/flask/) - Server
* [mongoDB](https://www.mongodb.com/) - Database

