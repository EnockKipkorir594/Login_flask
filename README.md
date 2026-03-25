#Flask Login Application
A simple web application with user authentication built python and flask, containerized with Docker

#Tech Stack
-**Python 3.12+**
-**Flask** - Web framework
-**Flask SQLAlchemy** - Database ORM 
-**Werkzeug Security** - Password hashing and verification 
-**Flask Sessions** - User session management 
-**SQLite** - Database
-**Docker** - Containerization 


##Project Structure 
'''
├── app.py                #App configs, database models, entry point 
├── bot.py
├── docker-compose.yml    #Docker compose config 
├── Dockerfile            #Docker image 
├── instance              #Database
│   └── test.db
├── myenv                 #Virtual environment 
│   ├── bin
│   ├── include
│   ├── lib
│   ├── lib64 -> lib
│   └── pyvenv.cfg
├── __pycache__
│   └── app.cpython-312.pyc
├── requirements.txt
├── static              #Contains css and images
│   └── css
└── templates           #HTML of the project 
    ├── base.html
    ├── dashboard.html
    ├── login.html
    └── registration.html
'''


##Features

-User registration with securely hashed passwords using werkzeug 
-Secure login and logout 
-Session-based authentication - User identity stored in flask sessions
-Protected routes - Redirect to login if no active session 

##How Authentication works 

This project handles authentication without any third party auth library.
Werkzeug and Flask sessions do all the heavy lifting:


**Registration**
'''python 
from werkzeug.security import generate_passord_hash
hashed_password = generate_password_hash(password)

**Login**
'''python 
from werkzeug.security import check_password_hash 
check_password_hash(user.password, password)

**Session**
from flask import session 

session['username'] = user.username 
session.pop('username', None)

if username not in session:
  return redirect('/login')

## Running Locally (Without Docker)

**1. Clone the repository**
```bash
git clone https://github.com/EnockKipkorir594/Login_flask.git
cd Login_flask
```

**2. Create and activate a virtual environment**
```bash
python -m venv venv

# Linux/Mac
source venv/bin/activate

# Windows
venv\Scripts\activate
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Run the application**
```bash
python run.py
```

Visit `http://localhost:5000` in your browser.

## Running With Docker

Make sure you have [Docker](https://www.docker.com/get-started) installed.

### Option 1 — Docker Compose (Recommended)
```bash
docker-compose up --build
```

Visit `http://localhost:5000` in your browser.

To stop the container:
```bash
docker-compose down
```

### Option 2 — Docker CLI

**Build the image**
```bash
docker build -t login-flask .
```

**Run the container**
```bash
docker run -p 5000:5000 login-flask
```

Visit `http://localhost:5000` in your browser.

## Dockerfile Overview
```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "run.py"]
```

- `FROM python:3.11-slim` — lightweight Python base image
- `WORKDIR /app` — sets the working directory inside the container
- `COPY requirements.txt` first — Docker caches this layer so dependencies
  are not reinstalled on every build unless requirements change
- `EXPOSE 5000` — documents that the app runs on port 5000
- `CMD` — the command that runs when the container starts

## Environment Variables

Create a `.env` file in the project root:
```bash
SECRET_KEY=your-secret-key-here
DATABASE_URL=sqlite:///users.db
```


## Author

**Enock Kipkorir**
[GitHub](https://github.com/EnockKipkorir594)




