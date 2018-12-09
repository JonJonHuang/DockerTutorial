# Creating a Simple Docker App
Lets say you want to write a simple application using Python 3.

1. Create a new directory and `cd` into it.
2. Create a new file and name it `Dockerfile`.
3. Write the following code in the file:

```docker
# FROM tells Docker which Docker libraries you are using
# Every Dockerfile should begin with a valid FROM statement
FROM python:3.7-slim
# Sets the working directory for your app within the Docker environment.
# COPY, RUN, and CMD all rely on WORKDIR
WORKDIR /app
# COPY copies the files within the source folder into the WORKDIR
COPY . /app
# RUN executes any command and commits the results to the Docker environment
RUN pip install --trusted-host pypi.python.org -r requirements.txt
# Makes port 80 available to the world outside this container, if needed
EXPOSE 80
ENV key value
# CMD provides default values for the execution of your app
# There can only be one CMD in a Dockerfile
CMD ["python", "app.py"]
```
4. You will also need a `requirements.txt` file where you will specify which pip packages you are using,
and an `app.py` file where you will write your Python code.  
Lets say that you are writing a web scraper using `requests-html`.  
Then in `requirements.txt` simply write the following line:
```
requests-html
```
5. Now you can write your web scraper code in `app.py`
```python
from requests_html import HTMLSession

session = HTMLSession()
response = session.get('http://www.fortunecookiemessage.com/')

print('Your fortune:', response.html.find('.quote')[0].full_text)
```
6. Build an image by running:
```bash
docker build -t fortunescraper ./
```
7. You've successfully built your first Docker image!
