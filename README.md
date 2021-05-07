# Creating_audio-file_server
Flask / FastAPI Web API that simulates the behavior of an audio file server while using a MongoDB / SQL database.
filed_audio_file_server
This is Test challenge by filed

##setup the system

Setup codebase

clone the code in a directory

 git clone https://github.com/NikhilRajChauhan/Creating_audio_file_server.git
go in the directory cd Creating_audio_file_server

install all project requirements, use command python -m pipenv install -r requirements.txt

go in pipenv virtualenv by python -m pipenv shell

set up flask env variable, run commands

set FLASK_APP=main.py
set FLASK_ENV=developement
create database

in postgresql create database "audioserver" and grant permission to user, in postgresql shell run command .

1. create db audioserver;
2. GRANT ALL PRIVILEGES ON DATABASE audioserver to "postgre"; # my username
create the table in audioserver database

in .env file add the data as below

# example
# DATABASE_URL="postgresql://postgre:abcdef08@localhost:5432/audioserver"
DATABASE_URL="postgresql://<username>:<password>@<server host>:<port>/<database name>
SECRET_KEY="this-is-a-sample-secret-key"
FLASK_ENV="development"
SQLALCHEMY_TRACK_MODIFICATIONS=True
lets do migrations, run following commands

flask db init
flask db migrate
flask db upgrade
this will create a migration folder, and create table in the database

run app, activate envrionment pipenv shell and run the command to run server flask run

check if server is running, in browser go to localhost:5000/, you will get server is running msg.

challenge Description
Write a Flask / FastAPI Web API that simulates the behavior of an audio file server while using a MongoDB / SQL database.

Requirements: You have one of three audio files which structures are defined below Audio file type can be one of the following:

1 – Song
2 – Podcast
3 – Audiobook
##Song file fields:

ID – (mandatory, integer, unique)
Name of the song – (mandatory, string, cannot be larger than 100 characters)
Duration in number of seconds – (mandatory, integer, positive)
Uploaded time – (mandatory, Datetime, cannot be in the past)
Podcast file fields:
ID – (mandatory, integer, unique)
Name of the podcast – (mandatory, string, cannot be larger than 100 characters)
Duration in number of seconds – (mandatory, integer, positive)
Uploaded time – (mandatory, Datetime, cannot be in the past)
Host – (mandatory, string, cannot be larger than 100 characters)
Participants – (optional, list of strings, each string cannot be larger than 100 characters, maximum of 10 participants possible)
##Audiobook file fields:

ID – (mandatory, integer, unique)
Title of the audiobook – (mandatory, string, cannot be larger than 100 characters)
Author of the title (mandatory, string, cannot be larger than 100 characters)
Narrator - (mandatory, string, cannot be larger than 100 characters)
Duration in number of seconds – (mandatory, integer, positive)
Uploaded time – (mandatory, Datetime, cannot be in the past)
API structuture is define in documentation folder. it is postman structure

Test challenge summary is define in documentation folder

##How to start

Clone the repo from github git clone https://github.com/NikhilRajChauhan/Creating_audio_file_server.git

in terminal go to folder , cd Creating_audio_file_server

setup flask app

 a. set FLASK_APP=main.py
 b. set FLASK_ENV='developement'
run flask server : flask run

check if server is running at browser localhost:5000/ you will get , server is running

How to TEST APIS
Test api structure is given in documentation, it is postman exported one.

apis end point
1. create
url = /api/v1/create 
method = Post
content-type=application/json
structures:
song

request body

 {
  "audioFileType":"song",
  "audioFileMetadata":{
      "uploaded_time":<upload time>>,
      "duration_time":<time duration in seconds>,
      "name":"<name of song>"
      }
  }
podcast

request body

 {
      "audioFileType":"podcast",
      "audioFileMetadata":{
              "uploaded_time":"0",
              "duration_time":102,
              "name":"in the end.mp4",
              "host":"linkin park - arizona park",
              "participents":["linkin park","us","american band"]
      }
   }      
audiobook

request body

  {
      "audioFileType":"audiobook",
      "audioFileMetadata":{
              "uploaded_time":"0",
              "duration_time":102,
              "title":"in the end.mp4",
              "author":"linkin park",
              "narrator":"linkin park"
      }
  }
####2. Update

url = /api/v1/update/<audioFileType>/<audioFileID> 
method = PUT
content-type=application/json
song

url : /api/v1/update/song/1

request body :

  {
      "audioFileType":"song",
      "audioFileMetadata":{
              "uploaded_time":"0",
              "duration_time":102,
              "name":"in the end - metoria by linkin park.mp4"    
      }
  }
podcast

url : /api/v1/update/podcast/1

request body :

  {
      "audioFileType":"podcast",
      "audioFileMetadata":{
          "uploaded_time":"0",
          "duration_time":102,
          "name":"linkin park in the end.mp4",
          "host":"linkin park - arizona park",
          "participents":["linkin park","us","american band"]    
       }    
}

audiobook

url : /api/v1/update/audiobook/1

request body:

  {
  "audioFileType":"audiobook",
  "audioFileMetadata":{
          "uploaded_time":"0",
          "duration_time":102,
          "title":"in the end.mp4",
          "author":"linkin park- mike shindoda",
          "narrator":"linkin park"  
  }
}

##3. delete

url = /api/v1/delete/<audioFileType>/<audioFileID>
method = DELETE
content-type = application/json
song
url: /api/v1/delete/song/1 - delete record present at id 1
podcast
url: /api/v1/delete/podcast/1 - delete record present at id 1
audiobook
url : /api/v1/delete/audiobook/1 - delete record present at id 1
##4. get

url: /api/v1/<audioFileType>
description: get all the data present in <audioFileType> database 2.- url: /api/v1/<audioFileType>/<audioFileID>
description: get all data present in <audioFileType> database having id audioFileID`
urls
song,

url1 = `/api/v1/get/song` - get all song in database
url2 = `/api/v1/get/song/1` - get song having id 1       
podcast

url1 = `/api/v1/get/podcast` - get all data in podcast in database
url2 = `/api/v1/get/podcast/1` - get song having id 1
audiobook

url1 = `/api/v1/get/audiobook` - get all data in audiobook in database
url2 = `/api/v1/get/audiobook/1` - get data having id 1
Return from REQUEST
- Action is successful: 200 OK
- The request is invalid: 400 bad request
- Any error: 500 internal server error
