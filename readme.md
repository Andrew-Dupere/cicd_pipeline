This is a CI/CD pipeline designed to be built on a Linux server so that pushes to the repo from 
a users local machine will atumoatically be pulled to the project on the Linux server

a shell script (sync.sh) runs the "git pull origin main" command

an api endpoint (webhook.py) runs the sync.sh script when a post request is made to the endpoint

make sure the correct port is open for a tcp connection (5000)

host the api using: nohup gunicorn --workers 3 --bind 0.0.0.0:5000 webhook:app &

test the endpoint/payload url using: curl -X POST http:<serverIP>:<PORT>/webhook

Add a webhook in github to autmoatically update the repository:
In Github settings find webhooks, use the api endpoint to update the payloard url and set content type to application/json

Additional steps may need to be taken such as setting up github access tokens and changing the permissions of the project directory.