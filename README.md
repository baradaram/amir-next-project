# AVC Sample Microservice

AVC Sample Microservice application written by Python3 & Django4.1

## Demo

___

First AVC Admin Service Initial Phase

## Technologies used in this service

___

- Python 3.x - Programming LanguageAdditional browser support

- Django 4.1.x - Powerful Web Framework

- GraphQl - Web API's

- Gunicorn - WSGI HTTP Server

- postgres - Postgresql Database

- NginX - High performance web server

- Docker - Container Platform

- GitHub - Version Control (initial phase)

- GraphQl Schema - API Documentation & Test

## Installation

___

1. Clone or download the project from GitHub:

       git clone  http://gl.mn.core:8082/avc_soft/globalusageservices/MS_Sample.git

2. Create necessary docker volumes and network:

       docker volume create --name=<service-name>_static_volume
       docker volume create --name=<service-name>_media_volume

       # should be create once (This is for base)
       docker network create --subnet 172.16.47.0/25 --gateway 172.16.47.126  avc_dev_base_network
    
       # should be create once (This is for base)
       docker network create --subnet 172.16.47.0/25 --gateway 172.16.48.126  avc_dev_base_network


3. you need to create .env.development file in the project settings file with default values.

       DEBUG=True
       SECRET_KEY=4=y_isy1#--i^spxqg72hdj=8_t=d6yi=je61*81v$ei00z*2
       ALLOWED_HOSTS=*
         
       POSTGRES_USER=postgres
       POSTGRES_PASSWORD=postgres
       POSTGRES_DB=Sample
       POSTGRES_HOST=192.168.23.49
       POSTGRES_PORT=5432
        
       CELERY_BROKER_URL = redis://:eYVX7EwVmmxKPCDmwMtyKVge8oLd2t81@192.168.23.49:6379/0
       CELERY_RESULT_BACKEND = redis://:eYVX7EwVmmxKPCDmwMtyKVge8oLd2t81@192.168.23.49:6379/0
        
       SERVICE_ID=<service-id>
        
       RABBITMQ_HOST=rabbitmq
       RABBITMQ_PORT=5672
       RABBITMQ_USERNAME=admin
       RABBITMQ_PASSWORD=admin
        
       QUEUE_NAME=<service-name>
       LOG_SERVICE_URL=http://192.168.23.47:8000/graphql
       NOTIFICATION_QUEUE=Notificaiton
        
       AWS_S3_ACCESS_KEY_ID=fB7tN1WMnkAPzciqkPOG
       AWS_SECRET_ACCESS_KEY=WxzjBKitDBoBViQLpEhx4LywKyj20PKVxWtwpWJM
       AWS_S3_ENDPOINT_URL=http://192.168.23.49:9000
       AWS_STORAGE_BUCKET_NAME=<service_name>


5. Now run django and postgres with docker-compose.

       docker-compose up -d

6. Then run nginx container with docker-compose.

       cd config/nginx/
       docker-compose up -d

7. You can see GraphQl Schema web page on http://localhost:8003/graphql . API's are accessable by docker containers
   which
   you can see with below command.

       docker ps -a

#### Output should be like this

CONTAINERS

       CONTAINER ID   IMAGE                   COMMAND                  CREATED        STATUS                         PORTS                                    NAMES 
      4dba0e8fb31b   avc_admin-admin          "gunicorn --chdir AV…"   4 minutes ago    Up 4 minutes                  0.0.0.0:8003->8003/tcp                 admin_app

nginx container as common web server, AVC_admin-admin container as django application .

# Test Style Guide

___

The project includes a suite of tests to ensure that all functionality is working correctly.

## Unit Tests

We use the pytest to write unit tests for individual functions and methods in our Django application. We ensured that
each component of our code was working correctly and met our requirements by testing them independently.

To run the unit tests, navigate to the root directory of the project and execute the following command:

    pytest

## Integration Tests

We used Factory Boy and Faker to create realistic data models that were used in our integration tests. These tests
helped us to ensure that all components of our application were working together correctly.

To run the integration tests, navigate to the root directory of the project and execute the following command:

    python manage.py test integration_tests/

## Scenario Tests

For scenario testing, we used Postman collections to simulate real-world scenarios for our Django backend API and
Knots / nodes . Our test cases covered a variety of endpoints ,knots / nodes and user workflows to ensure that our
application was functioning as expected.

To run the scenario tests, import the Postman collection provided in the tests directory and execute the requests in the
collection.

Senario Test Name Convention:

        [Service Name]_[Api Method Name]_[Request Type]_Collection.json

RabbitMQ
---
RabbitMQ is an open-source message-broker software that provides reliable messaging between distributed applications.
It implements the Advanced Message Queuing Protocol (AMQP) to provide reliable message delivery and routing.

## Style Guide

base on structure tree, each app has a broker directory which contains  `consumer.py`  and  `publisher.py` files. These
files are used to define the consumer and publisher logic for the app's message broker.


Code Style
---
Follow PEP 8 for Python code style.

- Use meaningful names for RabbitMQ-related objects such as queues, exchanges, bindings, etc.
- Use descriptive names for classes, functions, and variables.
- Use comments to explain complex code or document design decisions.
- Use docstrings to document functions and methods.
- Use meaningful commit messages when committing changes to version control.
- Keep your code clean and organized by following the directory structure outlined above.

# Directory Structure

___

The directory structure of the project is as follows:

- `project_name/`
    - `project_name/`
        - `__init__.py`
        - `celery_conf.py`
        - `commands.py`
        - `consumer.py`
        - `publisher.py`
        - `schema.py`
        - `settings.py`
        - `urls.py`
        - `wsgi.py`
    - `app1/`
        - `migrations/`
        - `broker/`
            - `publiser/`
                - `__init__.py`
                - `publiser.py`
            - `consumer/`
                - `consumer.py`
                - `__init__.py`
        - `tests/`
            - `__init__.py`

            - `scenario/`
                - `graphql/`
                    - `queries/`
                        - `scenario.json`
                    - `mutations/`
                        - `scenario.json`
                - `rest/`
                    - `get/`
                        - `scenario.json`
                    - `post/`
                        - `scenario.json`
                    - `put/`
                        - `scenario.json`
                    - `delete/`
                        - `scenario.json`
            - `unittest/`
                - `__init__.py`
                - `rest/`
                    - `__init__.py`
                    - `test_exdpoint1.py`
                - `graphql/`
                    - `__init__.py`
                    - `test_node.py`
            - `integration/`
                - `__init__.py`
                - `models/`
                    - `__init__.py`
                    - `test_model1.py`
                - `input/`
                    - `__init__.py`
                    - `test_input.py`
                - `objects_types/`
                    - `__init__.py`
                    - `test_objects_types.py`
                - `serializers/`
                    - `__init__.py`
                    - `test_serializers/`
                        - `__init__.py`
                        - `test_serializers.py`
        - `admin.py`
        - `apps.py`
        - `models.py`
        - `urls.py`
        - `views.py`
    - `utilities/`
        - `models.py`
        - `enum.py`
        - `utils.py`
    - `.gitignore`
    - `docker-compose.yml`
    - `Dockerfile`
    - `LICENSE`
    - `manage.py`
    - `pytest.ini`
    - `requirements.txt`
