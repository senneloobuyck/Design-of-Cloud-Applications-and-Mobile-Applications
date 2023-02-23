----
# Preparation 
## Hello world! 
Error occurred when creating new project using Python 3.7 
![[Pasted image 20230222152723.png]]

When creating new environment, I chose Python 3.9 and no errors occurred

Add imported packages to requirements:
![[Pasted image 20230222153026.png]]

Error when running the file: 
![[Pasted image 20230222180506.png]]

Jinja2 already installed 
![[Pasted image 20230222181223.png]]

In Python terminal: 
```
conda install --file requirements.txt
```

Laatste haakjes vergeten
![[Pasted image 20230222183822.png]]

![[Pasted image 20230222183856.png]]

## Returning sensor data as JSON

"webserver.py" 
```
from flask import Flask, jsonify  
from random import randint  
  
app = Flask(__name__)  
  
@app.route('/temperature')  
def temp_sensor():  
    value = randint(1, 40)  
    return jsonify({'temperature': value})  
  
@app.route('/light')  
def light_sensor():  
    value = randint(1, 100)  
    return jsonify({'light': value})  
  
if __name__ == '__main__':  
    app.run()
```

## Consuming our API

"webclient.py"
changed server URL from http://localhost:5000 to http://127.0.0.1:5000
```
import urllib.request  
from flask import Flask, json  
  
app = Flask(__name__)  
  
# URL of the webserver.py  
SERVER_URL = 'http://127.0.0.1:5000'  
  
@app.route('/')  
def index():  
    return 'Hello, World from client!'  
  
@app.route('/sensors')  
def sensors():  
    with urllib.request.urlopen(SERVER_URL + '/temperature') as resp:  
        temp_data = json.loads(resp.read().decode('utf-8'))  
    with urllib.request.urlopen(SERVER_URL + '/light') as resp:  
        light_data = json.loads(resp.read().decode('utf-8'))  
    return '<b>Temperature =</b> ' + str(temp_data['temperature']) + \  
    '<br><b>Light =</b> ' + str(light_data['light'])  
  
if __name__ == '__main__':  
    app.run(port=5001)
```

![[Pasted image 20230223135921.png]]

# First Flask application
* Flask depends on the Jinja2 engine
* Flask knows to look for HTML templates in the templates folder, and automatically configures the Jinja2 template engine for you.
* Static files holds CSS and JavaScript files that your web application might need for styling and formatting (give it a structure)
* Flask structure: 
![[Pasted image 20230223150440.png]]

- Bootstrap 
	* Popular open-source front-end framework for building responsive, mobile-first web applications
	* It provides a set of pre-designed CSS and JavaScript components, such as **container** (used in this lab)
		- <div class="container">



