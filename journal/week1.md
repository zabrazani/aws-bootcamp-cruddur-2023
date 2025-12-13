# Week 1 — App Containerization

## Switcing from ONA to Vscode  
I switched from ONA to vscode cos i could not port in ona which i later found out how to but did not matter any more.  
I downloaded and Installed Vscode
https://code.visualstudio.com/download  

I downloaded and installed Git so i can use Git Bash to clone my Github Repo  
https://release-assets.githubusercontent.com/github-production-release-asset/23216272/5fd8ab6c-2db0-462d-99bf-1c990b2d24a7?sp=r&sv=2018-11-09&sr=b&spr=https&se=2025-12-10T07%3A01%3A08Z&rscd=attachment%3B+filename%3DGit-2.52.0-64-bit.exe&rsct=application%2Foctet-stream&skoid=96c2d410-5711-43a1-aedd-ab1947aa7ab0&sktid=398a6654-997b-47e9-b12b-9515b896b4de&skt=2025-12-10T06%3A00%3A22Z&ske=2025-12-10T07%3A01%3A08Z&sks=b&skv=2018-11-09&sig=2LMhQODkzqTEFo0ORghi2Y957HT%2BHuIze37TFTNAdAE%3D&jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmVsZWFzZS1hc3NldHMuZ2l0aHVidXNlcmNvbnRlbnQuY29tIiwia2V5Ijoia2V5MSIsImV4cCI6MTc2NTM0ODk1MCwibmJmIjoxNzY1MzQ3MTUwLCJwYXRoIjoicmVsZWFzZWFzc2V0cHJvZHVjdGlvbi5ibG9iLmNvcmUud2luZG93cy5uZXQifQ.spcnnVeUzp4u_-JdKDxnOfM9mgl6bwdJ64lX2dxfy5k&response-content-disposition=attachment%3B%20filename%3DGit-2.52.0-64-bit.exe&response-content-type=application%2Foctet-stream  

I cloned my Github repo using Git Bash on my VsCode so i can work on my project with my local machine.  

![the view](assets/cloned%20repo.png)


## VsCode Docker Extention 
Docker extention for VsCode makes it so much easy to work with docker in VsCode.  
I installed the Docker Vscode Extention  
https://ms-azuretools.vscode-docker  

I created a dockerfile  and added comements
**  

I ran this code  
`RUN pip3 install -r requirements.txt`  
It failed  
`vscode ➜ /workspaces/aws-bootcamp-cruddur-2023/backend-flask (main) $ pip3 install -r requirements.txt`  
`bash: pip3: command not found`  
`vscode ➜ /workspaces/aws-bootcamp-cruddur-2023/backend-flask (main) $ `  

It failed because its a python package and i have try another way by downloading and installing python on my pc.  
1. Download http://python.com
2. During the Installion, check > Add Python to PATH
3. Verify Installion with: `python --version`


I ran the code again and it worked and installed.  

## Containized Backend  


### RUN PYTHON  

```sh
cd backend-flask
export FRONTEND_URL="*"
export BACKEND_URL="*"
python3 -m flask run --host=0.0.0.0 --port=4567
cd . .
```

- make sure to click on forward port at the port tab
- add 4567 in the port insert and open the link in your browser
- append to the url to '/api/activities/home'

## Add Docker File  

Create a file here:  `backend-flask/Dockerfile`  
```dockerfile
FROM  python:3.10-slim-buster

# Inside a container, set the working directory to /backend-flask
# This is where all the code will live
WORKDIR /backend-flask

# Outside Container -> inside Container
# this contains libraries to be installed to run the app
COPY requirements.txt requirements.txt

# Install python dependencies or libraries used in the app
# -r means read from a file
# 
RUN pip3 install -r requirements.txt

# Outside Container -> inside Container
# Copy everything from the current directory to the working directory in the container
# . means current directory
# first period . - /backend-flask (on your machine/outside container)
# second period . - /backend-flask (in the container/inside container)
COPY . .

# Set environment variables
# inside the container
ENV FLASK_ENV=development


EXPOSE ${PORT}

# Command to run the application
# python3 -m  flask run --host=0.0.0.0 --port=4567
#python -m flask run --host=0.0.0.0 --port=4567
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567" ]
``` 
## Unset the environmental variable
I unset the env var that I set earlier  
```sh
unset BACKEND_URL
unset FRONTEND_URL
```
To Verify 
```sh
env | grep BACKEND
env | grep FRONTEND
```

## Build Container  
`docker build -t backend-flask ./backend-flask`  



