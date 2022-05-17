#Dockerfile
FROM python:3.6
#install pip

RUN apt-get update && pip install pipenv
RUN python3.6 -m pip install aiohttp
RUN mkdir -p /opt/app

#copy source 
WORKDIR /opt/app/
COPY . . 

#start application
RUN pipenv install
ENTRYPOINT ["pipenv", "run", "python", "/opt/app/src/server.py"]
