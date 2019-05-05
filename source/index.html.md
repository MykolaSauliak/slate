---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  # - ruby
  # - python
  # - javascript

toc_footers:
  # - <a href='#'>Sign Up for a Developer Key</a>
  # - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# What's new

05.05.2019 - add quote and explanation field for Quiz

# Introduction

Welcome to the Quiz API! You can use our API to access Quiz API endpoints, which can get information on various quizpacks, quizzes in our database.

<!-- We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right. -->

<!-- This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation. -->

# Authorization

 We expects for the API key to be included in some API requests to the server in a header that looks like the following:

`Authorization: 9quizquizquiz9`

<aside class="notice">
You must replace <code>9quizquizquiz9</code> with your personal API key.
</aside> 

## Registration

To register new user, download our <a href="https://play.google.com/store/apps/details?id=com.kailuas.mnemonic">Android app</a>

## Recieve Authorization token

> To get Bearer token, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl -d "email=<youremail>&password=<password>"  -X POST "http://95.216.145.170:5000/api/users/login"

```
> Make sure to replace `<youremail>`with your registered email `<password>` with your password.

> The above command returns JSON structured like this:

```json
{
    "success": true,
    "token": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVjYWM2MTNmNDkyMTY5MTQ0MzJjNjg2ZCIsIm5hbWUiOiJuaWNrMiIsImlhdCI6MTU1NjQ4NTM5OCwiZXhwIjoxNTU2NDg4OTk4fQ.MJaRcH-vOWQpmpOMHPHzIov_skOGNgvFAbTs8OsfsFQ"
}
```

# Quizpacks

## Get All Quizpacks

```shell
curl "http://95.216.145.170:5000/api/quizpack"
```

> The above command returns JSON structured like this:

```json
[
    {
        "_id": "5c8f60211e909c5086d6a991",
        "title": "Переваги STP 2",
        "private": false
    },
    {
        "_id": "5cb0d9cefb6220631b12cb3a",
        "title": "Explore nanotechnology in the wild",
        "private": true
    }
]
```

<aside class="notice">
This endpoint retrieves only public quizpacks (private = false). To get private quizpack use next endpoint
</aside>


### HTTP Request

`GET http://95.216.145.170:5000/api/quizpack`

<!-- ### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted. -->

<!-- <aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside> -->

## Get a Specific (public) Quizpack 

```shell
curl -X POST "http://95.216.145.170:5000/api/quizpack/<ID>"
```

> The above command returns JSON structured like this:

```json
{
    "tags": [],
    "_id": "5ca26cb4746a040ba0f94983",
    "title": "ЩО ТАКЕ НАНОТЕХНОЛОГІЇ ? ",
    "user": "5c86a8ed622bc01844b77b90",
    "private": false,
    "password": "",
    "quizzes": [
        {
            "_id": "5ca26f83746a040ba0f9498d",
            "quiz": {
                "_id": "5ca26d0e746a040ba0f94984",
                "question": "Якими розмірами оперують нанотехнології ?",
                "type": "one-answer",
                "answers": [
                    {
                        "_id": "5ca26d0e746a040ba0f94987",
                        "answer": "від 5 до 200 нм",
                        "correct": "false"
                    },
                    {
                        "_id": "5ca26d0e746a040ba0f94986",
                        "answer": "від 1 до 100 нм",
                        "correct": "true"
                    },
                    {
                        "_id": "5ca26d0e746a040ba0f94985",
                        "answer": "від 10 до 100 нм",
                        "correct": "false"
                    }
                ],
                "user": "5c86a8ed622bc01844b77b90",
                "__v": 0
            }
        }
    ],
    "__v": 0
}
```

This endpoint retrieves a specific quizpacks.

<aside class="warning">
If the quizpack is private, you must send also password (see next endpoint)
</aside>

### HTTP Request

`POST http://95.216.145.170:5000/api/quizpack/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the quizpack to retrieve

## Get a Specific (private) Quizpack 

```shell
curl -d "password=quizpack_password" -X POST "http://95.216.145.170:5000/api/quizpack/<ID>"

Example:
curl -d "password=1234567" -X POST "95.216.145.170:5000/api/quizpack/5cc4af92a6f1412f6f89d366"

```


<aside class="notice">
You must replace <code>quizpack_password</code> with quizpack password, <code>ID</code> with quizpack's ID 
</aside>


> The above command returns JSON structured like this:

```json
{
    "tags": [],
    "_id": "5ca26cb4746a040ba0f94983",
    "title": "ЩО ТАКЕ НАНОТЕХНОЛОГІЇ ? ",
    "user": "5c86a8ed622bc01844b77b90",
    "private": false,
    "password": "",
    "quizzes": [
        {
            "_id": "5ca26f83746a040ba0f9498d",
            "quiz": {
                "_id": "5ca26d0e746a040ba0f94984",
                "question": "Якими розмірами оперують нанотехнології ?",
                "type": "one-answer",
                "answers": [
                    {
                        "_id": "5ca26d0e746a040ba0f94987",
                        "answer": "від 5 до 200 нм",
                        "correct": "false"
                    },
                    {
                        "_id": "5ca26d0e746a040ba0f94986",
                        "answer": "від 1 до 100 нм",
                        "correct": "true"
                    },
                    {
                        "_id": "5ca26d0e746a040ba0f94985",
                        "answer": "від 10 до 100 нм",
                        "correct": "false"
                    }
                ],
                "user": "5c86a8ed622bc01844b77b90",
                "__v": 0
            }
        }
    ],
    "__v": 0
}
```

This endpoint retrieves a specific private quizpack.

### HTTP Request

`POST http://95.216.145.170:5000/api/quizpack/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the quizpack to retrieve

### Body Parameters 

Parameter | Description
--------- | -----------
password | The password of the quizpack to retrieve

## Create a Quizpack

```shell
curl "http://95.216.145.170:5000/api/quizpack/add-quizpack"
  -X POST
  -d "title=newQUIZPACK&private=false"
  -H "Authorization: 9quizquizquiz9"
```

<aside class="notice">
You must replace <code>9quizquizquiz9</code> with your personal API key.

To get API key, use our endpoint (see <a href="#recieve-authorization-token">section</a> about)

</aside> 

<!-- <aside class="notice">
To get API key, use our endpoint (see <a href="#recieve-authorization-token">section</a> about)</aside>  -->


> The above command returns JSON structured like this:

```json
{
    "msg": "Successfully add newQuizPack",
    "id": "5cc60cf6907b972d25b651ba"
}

```

This endpoint create new quizpack.

### HTTP Request

`POST http://95.216.145.170:5000/api/quizpack/add-quizpack`

### Body Parameters

Parameter | Description | Default
--------- | ----------- | -----------
title* | The title of the new quizpack 
type* | one-answer or mulitple-choise 
private  | true or false | false
password | If you want to create private quizpack, set password (between 7 and 20 characters)
quizzes | Array of quizze's id <code>or</code> array of quiz objects | []
tags | Array of strings | []

> <aside class="notice">
Quiz object look like this :
</aside>

```json
{"question":"who is Boosh", "type" :"one-answer","answer1":"american president","answer2":"comedian","correct":["1"]}
```

## Delete a Quizpack

```shell
curl "http://95.216.145.170:5000/api/quizpack/<ID>"
  -X DELETE
  -H "Authorization: 9quizquizquiz9"
```
<aside class="notice">
You must replace <code>9quizquizquiz9</code> with your personal API key.
</aside> 

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : "ok"
}
```

This endpoint deletes a specific quizpack.

### HTTP Request

`DELETE http://95.216.145.170:5000/api/quizpack/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the quizpack to delete


## Modify a Quizpack

<aside class="notice">
Only user who created the quizpack can modify it
</aside>


```shell
curl "http://95.216.145.170:5000/api/quizpack/<ID>"
  -X PATCH
  -d "title=<newtitle>&tags=['new']"
  -H "Authorization: 9quizquizquiz9"
```
<aside class="notice">
You must replace <code>9quizquizquiz9</code> with your personal API key.
</aside> 

<aside class="notice">
Use params that you want to change, if you want to set new title, add to params - title=yourNewTitle
</aside>

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "modify" : "ok"
}
```

> Example, change quizpack's tags (you can send array of string or tags, separated by comma)

```shell
curl "http://95.216.145.170:5000/api/quizpack/5cc60cf6907b972d25b651ba"
  -X PATCH
  -d "tags=['new tag']"
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVjYWM2MTNmNDkyMTY5MTQ0MzJjNjg2ZCIsIm5hbWUiOiJuaWNrMiIsImlhdCI6MTU1NjUyNTkwMiwiZXhwIjoxNTU2NTI5NTAyfQ.iNc7fhn_IFvBeu9A43zycqCwXd9Y8bd5T-XjnXsTV4A"
```

This endpoint modify a specific quizpack.

### HTTP Request

`PATCH http://95.216.145.170:5000/api/quizpack/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the quizpack to modify



## Search Quizpacks

<aside class="notice">
User can also search private quizpack
</aside>


```shell
curl "http://api/quizpack/search"
  -X POST
  -d "searchString=test"
```

<!-- > The above command returns JSON structured like this:

```json
{
  "id": 2,
  "modify" : "ok"
}
``` -->

This endpoint search quizpacks.

### HTTP Request

`POST http://95.216.145.170:5000/api/quizpack/search`

### URL Parameters

Parameter | Description
--------- | -----------
searchString | Words that must be in title of quizpacks



## Add Quiz to the Quizpack

<aside class="notice">
We haven't endpoint to delete quiz from quizpack, to do this, try to use modify endpoint
</aside>


```shell
curl "http://api/quizpack/:quizpackID/addquiz/:quizID"
  -X POST
```

<!-- > The above command returns JSON structured like this:

```json
{
  "id": 2,
  "modify" : "ok"
}
``` -->

This endpoint add quiz to the quizpack.

### HTTP Request

`POST http://95.216.145.170:5000/api/quizpack/:quizpackID/addquiz/:quizID`

### URL Parameters

Parameter | Description
--------- | -----------
quizpackID | Quizpack id
quizID | Quiz id, quiz must be already created










# Quiz

## Create a Quiz

<!-- ```shell
curl "http://95.216.145.170:5000/api/quiz/add"
  -X POST
  -d "question=newQUIZPACK&type=one-answer&answer1=americanpresident&answer2=comedian&correct=['1']"
  -H "Authorization: 9quizquizquiz9"
``` -->

> The above command returns JSON structured like this:

```json
{
    "msg": "Successfully add newQuiz",
    "id": "5cc60cf6907b972d25b651ba"
}
```

This endpoint create new quiz.

### HTTP Request

`POST http://95.216.145.170:5000/api/quiz/add`

### Body Parameters

Parameter | Description | Default
--------- | ----------- | -----------
question* | The question of the new quiz 
type*  | one-answer or multiple-choice | 
answer1*  | String | 
answer2*  | String | 
answer3  | String | 
answer4  | String | 
answer5  | String | 
answer6  | String | 
correct* | Array correct answer (min =1,max=6) 
quote | String, max length 2000 characters
explanation | String, max length - 5000 characters

> <aside class="notice">
Quiz object look like this :
</aside>

```json
{"question":"who is Boosh", "type" :"one-answer","answer1":"american president","answer2":"comedian","correct":["1"]}
```

## Modify a Quiz

<aside class="notice">
Only user who created the quiz can modify it
</aside>


```shell
curl "http://localhost:5000/api/quiz/5cc60cf6907b972d25b651b7"  
-X PATCH -d "question=WhoIsBoosh&tags=['new']" -H "Authorization: Bearer ..."
```
<aside class="notice">
Use params that you want to change, if you want to set new question, add to params - question=yourNewQuestion
</aside>

> The above command returns JSON structured like this:

```json
{"_id":"5cc60cf6907b972d25b651b7","question":"WhoIsBoosh","type":"one-answer",
"answers":[
  {"_id":"5cc60cf6907b972d25b651b9","answer":"american president","correct":"false"},{"_id":"5cc60cf6907b972d25b651b8","answer":"comedian","correct":"false"}
],
"user":"5cac613f49216914432c686d","__v":0}  
```

This endpoint modify a specific quiz.

### HTTP Request

`PATCH http://95.216.145.170:5000/api/quiz/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the quiz to modify
