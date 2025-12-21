# Week 1 — App Containerization

## Switcing from ONA to Vscode  
I switched from ONA to vscode cos i could not port in ona which i later found out how to but did not matter any more.  
I downloaded and Installed Vscode
https://code.visualstudio.com/download  

I downloaded and installed Git so i can use Git Bash to clone my Github Repo  
https://git-scm.com/install/  

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

Well this command came with an error  
`docker build -t backend-flask ./backend-flask`  
`bash: docker: command not found`  

I had to download and install Docker Desktop and restart my pc.  
https://www.docker.com/products/docker-desktop/  

It still did not work.  
![](assets/error%20image.png)  

I had to update my wsl in my command prompt  
`wsl --update`  

I used `wsl -l -v` to verify my wsl is installed and updated and restarted my docker desktop..   

I ran the command  
`docker build -t backend-flask ./backend-flask`   

Finally it worked, you can see the download happening in the image.  
![](assets/Screenshot%202025-12-13%20013421.png)  

## Run Container  

### Run  

`docker run --rm -p 4567:4567 -it backend-flask`  

### Run in the Background  

`docker container run --rm -p 4567:4567 -d backend-flask`
`FRONTEND_URL="*" BACKEND_URL="*" docker run --rm -p 4567:4567 -it backend-flask`  

### I noticed that there is nothing on my container but the image is showing  
I used this command  
`docker run -p 4567:4567 -d --name cruddur-backend backend-flask:latest`  
It is working  
![Here it is](assets/Cont%20showed.png)  

### Back to Run in the background

Since `FRONTEND_URL="*" BACKEND_URL="*" docker run --rm -p 4567:4567 -it backend-flask` did not work and I tried troubleshooting it  
I left click the backend-flask:latest contianer and clicked on view logs to show the logs  
other solution I keft click the container again and clicked on the attach shell to bring up the container root shell  
After i used `env` to check my environmental variable and its not there.

to get docker help  
`docker run --help`  
> --env list     Set environment variables

Then I used this commands to successfully resolve our environmental Issue problem and successfully run the code and i saw my container.  
```sh
set BACKEND_URL="*"  
set FRONTEND_URL="*"  
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
# or
docker run --rm -p 4567:4567 -it  -e FRONTEND_URL -e BACKEND_URL backend-flask
unset BACKEND_URL="*"
unset FRONTEND_URL="*" 
```

### Get Container Images  or Running Container  Ids  

```
docker ps
docker images

```

### Send Curl to Test Server 
### Send a GET Request (Default) 
` curl https://tcfbzj88-4567.uks1.devtunnels.ms/api/activities/home `  
###  Send a POST Request with Data (e.g., JSON)  
`curl -X POST -H "Content-Type: application/json" -d '{"key": "value", "another_key": "another_value"}' https://tcfbzj88-4567.uks1.devtunnels.ms/api/activities/home`  
### Send a PUT Request (Update Data)  
`curl -X PUT -H "Content-Type: application/json" -d '{"updated_key": "updated_value"}' https://tcfbzj88-4567.uks1.devtunnels.ms/api/activities/home`  
### Upload a File  
```
curl -T localfile.txt ftp://tcfbzj88-4567.uks1.devtunnels.ms/api/activities/home
# Or via HTTP, if the server accepts PUT requests for upload
curl -X PUT -T localfile.txt https://tcfbzj88-4567.uks1.devtunnels.ms/api/activities/home
```
### Add Authentication  
` curl -u username:password https://tcfbzj88-4567.uks1.devtunnels.ms/api/activities/home`  

### Check Container Logs  
```
docker logs <container-name-or-id>
docker logs -f <container-name-or-id>
docker logs -t <container-name-or-id>
docker logs -t <container-name-or-id>
docker logs --since=1h <container-name-or-id>

```

###Gain Access to a Container  
`docker exec CONTAINER_ID -it /bin/bash`  

### Delete An Image  
Stop and remove containers (if necessary): If the image is in use by a container (even a stopped one), you must remove the container first  
```sh
# List all containers (running and stopped)
docker ps -a
# Stop a running container
docker stop <container_id_or_name>
# Remove the container
docker rm <container_id_or_name>

```
Delete the image: Use the docker rmi command with the image's name (repository:tag) or Image ID.  
```sh
docker rmi <image_name>:<tag>
# or using the image ID (first few digits usually suffice)
docker rmi <image_id>

```
If you need to force the removal (e.g., if a running container is using it and you want to bypass the error), use the -f (force) flag.  
` docker rmi <image_id_1> <image_id_2> <image_name_3> `

## Containernize Frontend  

### Run NPM Install  
We have  to run NPM install before building  the container since it needs to copy  the contents  to node_modules  
```
cd frontend-react-js/
npm i
```
i for install

My `npm i` did not work so i ahve to download and install node.js, restart my computer.
https://nodejs.org/en/download  
> make sure when installing node.js you select 'ADD PATH' Option

  

### Create Dockerfile  
Create a file here `frontend-react-js/Dockerfile `  

```
# --- ADD THIS LINE (The Missing Base Image) ---
FROM node:18-alpine 
# ---------------------------------------------
COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm  install
EXPOSE ${PORT}
CMD ["npm", "start"]
```
## Multiple Container  
### Create a docker-compose.yaml  
Create a docker-compose.yaml  
```yaml
version: '3.8'

services:
  backend-flask:
    environment:
      # --- FIX 1: Use localhost/IP addresses for local host communication ---
      FRONTEND_URL: "http://localhost:3000" 
      BACKEND_URL: "http://localhost:4567" 
    build: ./backend-flask
    # Note: If 4567 is busy, you can change the host port, e.g., "4568:4567"
    ports:
      - "4567:4567"
    volumes:
      - ./backend-flask:/backend-flask
    # --- FIX 3: Add this line to ensure services can communicate within the network ---
    networks:
      - internal-network

  frontend-react-js:
    environment:
      # --- FIX 2: Use the service name for backend communication ---
      REACT_APP_BACKEND_URL: "http://backend-flask:4567" 
    build: ./frontend-react-js
    # frontend will be accessible on your browser at http://localhost:3001
    ports:
      - "3001:3000"
    volumes:
      - ./frontend-react-js:/frontend-react-js
    # --- FIX 3: Add this line to ensure services can communicate within the network ---
    networks:
      - internal-network

# The network definition should remain at the end
networks:
  internal-network:
    driver: bridge 
    name: cruddur
```

To get it running
`docker-compose up`  
or  
left click on the docker-compose file and click on the compose up option.  

And we have data!  

![](assets/Screenshot%20(5795).png)  

Also use docker compose down to shut it down... thank you  



## week - 1 - Add postgress Dynamodb  

### Adding DynamoDB  Local and Postgres  

We are going to use Postgres and DynamoDB local in future labs. We can bring them in as containers and reference them externally  

Let's Intergrate following into our existing docker compose file

### DynamoDB Local  

```yaml
services:
dynamodb-local:
  # https://stackoverflow.com/questions/67533058/persist-local-dynamodb-data-in-volumes-lack-permission-unable-to-open-databa
  #We needed to add user:root to get  this working..
  user: root
  command: "-jar DynamoDBlocal.jar -sharedDb -dbPath ./data"
  image: "amazon/dynamodb-local:latest"
  container_name: dynamodb-local
  ports:
    - "8000:8000"
  volumes:
    -"./docker/dynamodb:/home/dynamodblocal/data"
  working_dir: /home/dynamodblocal
```

[Documents about Dynamodb](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.DownloadingAndRunning.html)

Examples of using Dynamodb Local  
[](https://github.com/zabrazani/aws-bootcamp-cruddur-2023/blob/main/Challenge%20DynamoDB%20Local)

### Postgres  

```yaml
services:
  db:
    Images: postgres:13-alpine
    restart: always
    environment:
      - POSTGRES_USER postgres
      - POSTGRES_PASSWORD password
    ports:
      - "5432:5432"
    volumes:
      - db:/var/lib/postgresql/data
  volumes:
    db:
      driver:local
```

How to install the postgres client on gitpod  
```sh
- name: postgres
    init: |
      curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
      echo "deb http://apt.postgresql.org/pub/repos/apt/ 'lsb_release -cs'-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list
      sudo apt-get update
      sudo apt install -y postgresql-13 libpq-dev
```
## How to Install on Vscode/Windows/Linux-Mac  

Got it — you want to use a **Postgres client inside VS Code** so you can connect to your PostgreSQL database directly. There are two main approaches:

---

## 🛠 Option 1: Install a VS Code Extension (Recommended)
The easiest way is to use a database extension that integrates PostgreSQL into VS Code.

### Steps:
1. Open **VS Code**.
2. Go to the **Extensions Marketplace** (`Ctrl+Shift+X`).
3. Search for **PostgreSQL**.
   - Popular choices:
     - **PostgreSQL** (by Chris Kolkman) – lightweight client.
     - **SQLTools** + **SQLTools PostgreSQL Driver** – more advanced, supports multiple databases.
4. Install the extension.
5. Open the **Command Palette** (`Ctrl+Shift+P`) → search for **PostgreSQL: Add Connection**.
6. Enter your connection details:
   - **Host:** `localhost`
   - **Port:** `5432`
   - **User:** `postgres`
   - **Password:** `password` (or whatever you set in Docker)
   - **Database:** `postgres` (default)

Now you can run queries directly inside VS Code.

---

### 🛠 Option 2: Install the Postgres CLI (`psql`)
If you want the **command-line client** available in VS Code’s terminal:

### Windows
1. Download **PostgreSQL installer** from [https://www.postgresql.org/download/windows/](https://www.postgresql.org/download/windows/).
2. During installation, check the box for **Command Line Tools**.
3. Add PostgreSQL’s `bin` folder to your **PATH** (e.g., `C:\Program Files\PostgreSQL\18\bin`).
4. Restart VS Code → open terminal → run:
   ```bash
   psql -h localhost -U postgres -d postgres
   ```

### Linux / macOS
```bash
sudo apt install postgresql-client   # Ubuntu/Debian
brew install postgresql              # macOS (Homebrew)
```

---  
  

##Here’s how to set it up properly On Windows:

---

### 🛠 Steps to Add PostgreSQL to PATH on Windows
1. **Locate the bin folder**  
   - By default, PostgreSQL installs under:  
     ```
     C:\Program Files\PostgreSQL\<version>\bin
     ```
   - For example:  
     ```
     C:\Program Files\PostgreSQL\18\bin
     ```

2. **Add to PATH**  
   - Press **Win + R**, type `sysdm.cpl`, and hit Enter.  
   - Go to **Advanced → Environment Variables**.  
   - Under **System variables**, find `Path` → click **Edit**.  
   - Click **New** → paste:  
     ```
     C:\Program Files\PostgreSQL\18\bin
     ```
   - Click **OK** to save.

3. **Verify in VS Code Terminal**  
   - Restart VS Code (important so it reloads environment variables).  
   - Open a terminal and run:  
     ```bash
     psql --version
     ```
   - You should see something like:  
     ```
     psql (PostgreSQL) 18.x
     ```

---

## ⚡ Why This Matters
Adding the `bin` folder to PATH lets you run PostgreSQL tools (`psql`, `createdb`, `pg_dump`, etc.) directly from **any terminal**, including VS Code’s integrated terminal, without needing to type the full path.

---





