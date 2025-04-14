# Simple Survey API

## Tools

- [Flask](https://flask.palletsprojects.com/en/stable/)
- [Postgres](https://www.postgresql.org/)

## Project Setup

### Development

1. Create a Postgres database locally and name it `sky_survey_db`
2. Create a `.env` file in the root directory and add the following environment variables:

```
DATABASE_USERNAME=<your_database_username>
DATABASE_PASSWORD=<your_database_password>
DATABASE_NAME=sky_survey_db
DATABASE_HOST=localhost
DATABASE_PORT=5432
```

3. Create a virtual environment and activate it

4. Install the dependencies by running

```sh
pip install -r requirements.txt
```

5. Initialize the database by running the following commands:

```sh
flask db init
flask db migrate
flask db upgrade
```

6. On the root directory, create a new file and name it `.flaskenv`. Add the following flask environment variables to the file:

```
FLASK_APP=flaskr
FLASK_DEBUG=True
```

7. Run the following command to start the server:

```sh
flask run
```

### SQL Script Generation

Run the following command in the terminal (Linux distributions)

```sh
pg_dump -U postgres -d sky_survey_db --password -f sky_survey_db.psql
```

## Deployment

This repo consists of a Flask application which serves as the API between the client and the deployed relational database managed by the [AWS RDS](https://aws.amazon.com/rds/?trk=492c57d3-8cdc-4660-b6ac-d2008bd51b40&sc_channel=ps&ef_id=CjwKCAjw5PK_BhBBEiwAL7GTPYvfE-DRkWRR036jPwXq-GEInzvUkodV92gS-IA5lWtfaqChbbj3rBoCPi0QAvD_BwE:G:s&s_kwcid=AL!4422!3!645125273492!e!!g!!aws%20rds!19574556899!145779850032&gbraid=0AAAAADjHtp_uRM_dqUKpcoLbobJijevOw&gclid=CjwKCAjw5PK_BhBBEiwAL7GTPYvfE-DRkWRR036jPwXq-GEInzvUkodV92gS-IA5lWtfaqChbbj3rBoCPi0QAvD_BwE) service.

The Flask application is deployed on [Render](https://render.com/).

The deployment process is streamlined by connecting Render to the application's remote repo on Github. The process works as follows:

1. Developer makes a change in a separate branch and pushes the changes to the remote repo.
2. Developer raises a PR to the `development` or `main` branch
3. Once the reviewer approves the changes, the PR is merged to the `main` branch.
4. Render detects the changes on the `main` branch, builds and deploys the Flask application to the production environment.

- The service can be accessed using the following API endpoint: [Sky World Survey API](https://sky-world-survey-api.onrender.com)
> The instance runs on a free tier service on Render. Initial API calls to the API might delay for about 60 seconds by returning a 502 Bad Gateway response.
