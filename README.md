
# Django-request-counter

Install this app to get django api request count


## Installation

Install my-project with pip

```bash
  pip install request-counter
```
In settings.py add below
Add the app in installed apps 
```
INSTALLED_APPS = [
    ...
    "request_counter",
]
```
Add middleware
```
MIDDLEWARE = [
    ...
    "request_counter.middlewares.APICounterMiddleware",
]
```
To check using API Add
```
urlpartterns = [
    ...
    path("",include("request_counter.urls")),
]
```
Set environment variable in settings.py file
```
# set up redis ur;
# REDIS_URL = "redis://localhost:6379/7" # by default when not set
REDIS_URL = "<your redis url path>"

# api path that starts with that needs monitoring
RC_API_START_PATH = "/api/" # by default set "" for monitoring all path default /api/ when not set 
RC_API_START_PATH = "<your starting path>"

# database where you want to store the result after running script
# RC_DATABASE = "default" # by default it is set as default database when not set
RC_DATABASE = "<your desired database>"

# when saving on 1 database but have many environment
RC_ENVIRONMENT = "" # add prefix on your database path to identify
RC_ENVIRONMENT = "<your environment>"

RC_REDIS_EXPIRE_SECONDS = 86400 # redis key ttl expiry seconds

```
You need to setup cron to periodically save the data into default database 
```
python manage.py store_api_count
```

Now make api request with admin user
```
curl --location '<base-url>/api-count/' \
--header '<your authentication header>'

curl --location '<base-url>/api-count/redis' \
--header '<your authentication header>'
```