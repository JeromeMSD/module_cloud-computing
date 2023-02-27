[🇫🇷 Version française](SUJET_PROJET.md)

[![uB](img/UB.png)](https://u-bourgogne.fr/) | ESIREM - 4A - ILC/SQR <br/> Cloud computing <br/><br/> **[ PRATIQUE EXAM ]** | [![ESIREM](img/ESIREM.png)](https://esirem.u-bourgogne.fr/)
:--- | :---: | ---:
|| End of project set at `April 7, 2023 at 11:59pm` ||

Table of content
---

* [Project\'s topic](#projects-topic)
* [Exigences projet](#project-requirements)

---

Practice exam for CI/CD module will evaluate skills and development good practice see in class. The final grade will be based on API's functionality, meeting the project requirements, your understanding of your code and collaboration within developper pair.

---

# Project's topic

[![Twitter](https://upload.wikimedia.org/wikipedia/commons/thumb/5/51/Twitter_logo.svg/2560px-Twitter_logo.svg.png)](https://twitter.com)

<br/>

Throughout this project, you're gonna implement microservices components to remake **Twitter** SaaS ☝️

## Project's steps

### Pre cleanning 

Use you directed work repository. ( can be renamed if needed ) 
Move your previous work ( files, folders and README.md ) to a folder `TD` at root of repository.

Create a new README.md file at root.

In this file you will add project realization's details, binomial members, used languages, badges, status badges with last workflows outputs (passed/failed) and a explaination to how to start the project components on a computer.

The repository will be organized with two folders at root beside `README.md` file :

* one named `frontend` for user interface development.
* one named `backend`, for API's code.

Each will have a specific **README** and a **Dockerfile** to start microservice's component within a containers.

> You don't need `swagger.yaml` file for this project.

---

### API 🚀

The API is a brain for your SaaS, an application programming interface which realize actions. requests send to API are treated and result informations is send back to user. Either with a tool like `curl` or hide in javascript function of a `frontend`, sending request to API allow to execute action on data.

Implement a simple API ( `Python/Flask`, `Node` or `Rust` ). Which allow to perform following features using `GET` and `POST` HTTP method :

* Display tweets.
* Save a tweet ( in `Redis` ).
* Display tweets of a user.
* Retweet.
* Display topics (hashtags).
* Display tweets of a topic.

#### Hashtags

Topics can be managed by creating topic dedicated key in author dictionnary.

*For example* : You can prefix to avoid conflict and overwriting of keys. Say `u-username` for users and `h-hashtag` for topics.

> **[ Tips ]** To filter and sorts hashtags, users and tweets, use the corresponding endpoint function.

ℹ️ Use can implement your own format for topics, users and tweet management, precise your choice in README file.

#### Send complex object in request

To send and return data between fronend and API, HTTP requests and responses can be simplified using [`JSON`](https://fr.wikipedia.org/wiki/JavaScript_Object_Notation) structures. You will be able to treat or transform data or message through API endpoint's functions.

> **[ Tips ]** Before using directly `Redis` you can use dictionnary variables to tests your endpoints and associated features. 

Test your endpoints with `curl` command.

---

### Redis

To externalise data storage and ensure there persistency in API restart, use `redis`.

#### What's Redis ?

`Redis` is a key/value database which allow to quickly store data using dicitonnaries.

Use `Redis` as database start in a container on your device. It can be access using `localhost` on `6379` port.

In a other prompt, start `redis` foreground using the following command :

```bash
docker run --name myredis -p 6379:6379 redis
```

> Tips : use `redis-cli` tool to access to `redis` directly without `python` script.

If you were storing tweets in dict variable, you can now replace it with your containerized `redis` serveur.

#### Store tweets in Redis

Store your tweets in two databases.

First one with tweets.

*example :* `key=timestamp, value=’{“author”: “username”, “tweet”: ”message”}’`

The other with users and topics where keys are usernames or topics and values are tables to tweet's keys.

*exemple :* `key=username, value=[timestamp_1, timestamp_2, timestamp_3]`

This architecture is an example. You're free to choose another one but make it work 😉

---

### Everything is in the detail 🧐

Now you need a user interface !

With the language of your choosing ( `HTML/CSS/JS`, `Node`, `VueJS`, `React`… ) create a `frontend` to request your API. Using boutons and forms, it must be able to call actions of your API and display responses.

Let your imagination run wild when designing your Twitter, display doesn't matter but it must cover **every features of the API** (cf. [API 🚀](#api-🚀))

ℹ️ Don't forget the **Dockerfile** to start it within container.

ℹ️ You'll describe `frontend` features within **README.md** of `frontend` folder.

---

## Project requirements

End of project is set at `7 avril 2023 à 23h59`.

> No changes on repository or in the code will be considered after this date

### GitHub

You must store your code in a GitHub repository where you've added my as collaborator.

* Changes history of the repository must show collaboration within group members ( commit from different users on project files ).
* A GitHub Action on every `push` to `build` or check API syntax (*cf. CI/CD project*).
* 3 READMEs within repository : one for `frontend`, one for `backend` and the main one at root.
* Main README must contain **project realization's details**, **binomial members**, **used languages**, **badges**, **status badges** with last workflows outputs (passed/failed) and a explaination to how to start the project components on a computer.

> You don't need `swagger.yaml` file for this project.

### Docker

* One Dockerfile to build API (`backend`).
* One Dockerfile to build `frontend` if you're using `Node`, `React` or `VueJs`.

> **[ Tips ]** If you're using `HTML/CSS/JS` use a `nginx` Dockerfile.

### Redis

* Describe your database structure in **backend's README**.
* Create a `python` script to load in `redis` tweets and default users. This script will allow me to tester user interface.

### User Interface

* Describe covered features in **fronend's README frontend**.

### backend API

* Describe covered features in **backend's README**.
