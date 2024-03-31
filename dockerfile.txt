FROM python:3.10-slim-buster

ENV PYTHONUNBUFFERED=1
EXPOSE 8000

WORKDIR /apps
COPY . .


RUN pip install poetry
RUN pip install requirements
RUN poetry config virtualenvs.create false
RUN poetry update
RUN python manage.py migrate
RUN chmod 744 ./startup.sh

ENTRYPOINT ["./startup.sh"]