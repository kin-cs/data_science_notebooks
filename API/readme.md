Some API tutorial
===

- Basic Linear Regression model with simple preprocessing with prediction input:
  - blog: https://www.datacamp.com/community/tutorials/machine-learning-models-api-python
  - code: https://github.com/amirziai/sklearnflask/blob/master/main.py
- Simple examples:
  - https://hackernoon.com/deploy-a-machine-learning-model-using-flask-da580f84e60c
  - https://medium.freecodecamp.org/a-beginners-guide-to-training-and-deploying-machine-learning-models-using-python-48a313502e5a
  - https://towardsdatascience.com/deploying-a-machine-learning-model-as-a-rest-api-4a03b865c166
- Video mid-level example:
  - https://www.youtube.com/watch?v=-UYyyeYJAoQ
- Deploy ML Models using Flask, Docker and Google Cloud Platform
  - https://medium.com/analytics-vidhya/how-to-deploy-machine-learning-models-using-flask-docker-and-google-cloud-platform-gcp-6e7bf1b339d5
- Make Jupyter Notebook to consume the API call:
  - https://ndres.me/post/jupyter-notebook-rest-api/
  - https://blog.ouseful.info/2017/09/06/building-a-json-api-using-jupyer-notebooks-in-under-5-minutes/

#### Keywords
- Swagger - open-source software framework backed by a large ecosystem of tools that helps developers design, build, document, and consume RESTful Web services- https://swagger.io
  
### Notes:
- flask’s inbuilt server is not suitable for production as it doesn’t scale well. You’ll need to use a WSGI server to run your flask application. eg. gunicorn, uwsgi.

Issues to consider:
===
- put it in Docker
- Versioning
- Workload scaling
- Connection to DB
- Logging
- Crashes and recovery / Zero downtime deployment
- etc.

Error Handling by Flask
===
- Easy example: https://flask-restplus.readthedocs.io/en/stable/errors.html
- Verbose example: http://shzhangji.com/blog/2018/04/07/error-handling-in-restful-api/ 
#### Flask abort()
- it will handle the error with simple HTTP output. Unlock Werkzeug before using it [link](https://github.com/django-extensions/django-extensions/issues/787)

Production Concept
===
- High level concept of steps in Production: https://machinelearningmastery.com/deploy-machine-learning-model-to-production/

Using HTTPS (SSL)
---
- https://blog.miguelgrinberg.com/post/running-your-flask-application-over-https

Snippets:
===
- To POST a request in python
```python
import requests
url = 'http://localhost:5000/api'
r = requests.post(url,json={'exp':1.8,})
print(r.json())
```

Ref
---
- https://www.youtube.com/watch?v=-UYyyeYJAoQ
