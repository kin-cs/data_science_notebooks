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
- ref: http://shzhangji.com/blog/2018/04/07/error-handling-in-restful-api/ Example below
```python
class BadRequest(Exception):
    """Custom exception class to be thrown when local error occurs."""
    def __init__(self, message, status=400, payload=None):
        self.message = message
        self.status = status
        self.payload = payload


@app.errorhandler(BadRequest)
def handle_bad_request(error):
    """Catch BadRequest exception globally, serialize into JSON, and respond with 400."""
    payload = dict(error.payload or ())
    payload['status'] = error.status
    payload['message'] = error.message
    return jsonify(payload), 400


@app.route('/person', methods=['POST'])
def person_post():
    """Create a new person object and return its ID"""
    if not request.form.get('username'):
        raise BadRequest('username cannot be empty', 40001, { 'ext': 1 })
    return jsonify(last_insert_id=1)
```


Production Concept
===
- High level concept of steps in Production: https://machinelearningmastery.com/deploy-machine-learning-model-to-production/

Using HTTPS (SSL)
---
- https://blog.miguelgrinberg.com/post/running-your-flask-application-over-https

----
Ref
---
- https://www.youtube.com/watch?v=-UYyyeYJAoQ
