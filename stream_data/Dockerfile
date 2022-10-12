FROM python:3.9
COPY ./src /home
WORKDIR /home
RUN pip3 install -r requirements.txt
CMD [ "python3", "./airquality.py" ]
