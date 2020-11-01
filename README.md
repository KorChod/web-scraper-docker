# Web Scraper
Web scraper project. Service is responsible for downloading content from a given page (text and images) and saved in a databse. Necessary information was scraped with a Python library BeautifulSoup. Each request is handled asynchronously with Celery and broker RabbitMQ. Application was containerized with Docker for easier dependency and library management.

## Tech Stack
- Python
- Django / Django REST Framework
- Celery
- RabbitMQ
- Docker

## Implemented features
Following API endpoints were created:
- '/api/scrape/text/': handling POST request method. Responsible for downloading text from a specified page. "Url" value must be provided in the request's body;
- '/api/webpages/': handling GET method. Displays list and details of previously downloaded pages. "OffsetPagination" class was used so that user can customize displayed ranges;
- '/api/webpages/<webpage_id>/: handling GET method. Displays details for a particular page;
- '/api/task/<task_id>/: handling GET method. Displays current status of a particular asynch download task;

Additionally all functionalities were covered with unit tests. For this purpose "unittest" library was used and APITestcase class.

## Setup
- to launch this project one has to build a docker image and run container by executing the following command: `docker-compose up`.
- next step is to make data migration. In a separate terminal window execute `docker-compose run --rm python bash` command. Now, inside the running container, create migrations with `python manage.py makemigrations` and then migrate `python manage.py migrate`.
- application should be running now. You can try to access any of the previously mentioned routes in your browser.
