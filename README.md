# Actually, let's do it another way
### This project starts by creating a Django app, then running create-react-app inside. I ran into issues trying to deploy this to heroku, so I found a better way to do it.

### Run create-react-app first, then start the django app in the same directory. The new project can be found here:
### https://github.com/bmiczek/react-django-boilerplate

---

# Django React Boilerplate Setup
Reference this pull request while following the below steps: https://github.com/bmiczek/django-react-boilerplate/pull/1

## 1. Create the Django backend app
### 1.1. Create the project folder
```
git clone <repository_url>
# OR
mkdir <project-name>

cd <project-name>
```
### 1.2. Setup python virtual environment
```
pyenv virtualenv <project-name>
pyenv local <project-name>
```
### 1.3. Install django and create the project
```
pip install django
django-admin startproject backend .
```
### 1.4. Run migrations and start server
```
./manage.py migrate
./manage.py runserver
```
Go to http://127.0.0.1:8000/

## 2. Create the React frontend app
### 2.1. Run create-react-app
```
npx create-react-app frontend
cd frontend
```
### 2.2. Eject from create-react-app

Eject requires you to first commit your repo to git
```
git commit -am 'checkpoint before eject'

npm run eject
```

### 2.3. Start the server
```
npm run start
```

Go to http://localhost:3000/

## 3. Setup backend
### 3.1. Install django-webpack-loader
```
cd <project-root>
pip install django-webpack-loader
pip freeze > requirements.txt
```
### 3.2. Modify backend files to use webpack-loader
Check the [pull request](https://github.com/bmiczek/django-react-boilerplate/pull/1) for changes in:
```
.gitignore
backend/
templates/index.html <- copied and modified from frontend/index.html
assets/ <- copied from frontend/public/
```

## 4. Setup frontend
### 4.1. Install webpack-bundle-tracker
webpack-bundle-tracker alpha version (or greater) required for webpack 4 support
```
cd frontend
npm install --save-dev webpack-bundle-tracker@1.0.0-alpha.0
```
### 4.2. Create .env file
```
cp .env.sample .env
```

### 4.3. Modify frontend files to use webpack-bundle-tracker
Check the [pull request](https://github.com/bmiczek/django-react-boilerplate/pull/1) for changes in:
```
frontend/config/
```

## 5 Run dev server
### 5.1. Start the npm server
```
cd frontend/
npm start
```
### 5.2. Start the python server
```
cd ..
./manage.py runserver
```

## 6 Run production build
### 6.1. Build the frontend bundle
```
cd frontend/
npm build
```

### 6.2. Start the python server with production settings
```
cd ..
./manage.py runserver --settings=backend.settings_production
```
