FROM python:3.7.5-slim-buster

RUN mkdir /app
WORKDIR /app

RUN apt-get update -y && apt-get install -y \
	python3-pip \
	python3-dev \
	libsm6 \
	libxext6 \
	libxrender-dev
RUN pip3 install --upgrade pip

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

LABEL maintainer="Farhad Ullah Rezwan frez0003@student.monash.edu" \
version="1.0"

CMD flask run --host=0.0.0.0 --port=5000 
