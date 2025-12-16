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
