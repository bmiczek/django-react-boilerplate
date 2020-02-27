# Django React Boilerplate Setup

## 1. Create the Django backend app
### Create the project folder
```
git clone <repository_url>
# OR
mkdir <project-name>

cd <project-name>
```
### Setup python virtual environment
```
pyenv virtualenv <project-name>
pyenv local <project-name>
```
### Install django and create the project
```
pip install django
django-admin startproject backend .
```
### Run migrations and start server
```
./manage.py migrate
./manage.py runserver
```
Go to http://127.0.0.1:8000/

## 2. Create the React frontend app
```
npx create-react-app frontend
cd frontend
```
### Eject from create-react-app

Eject requires you to first commit your repo to git
```
git commit -am 'checkpoint before eject'

npm run eject
```

### Start the server
```
npm run start
```

Go to http://localhost:3000/

## 3. Setup backend
### Install django-webpack-loader
```
cd <project-root>
pip install django-webpack-loader
pip freeze > requirements.txt
```
### Modify backend files to use webpack-loader
Check the pull request for changes in:
```
.gitignore
backend/
templates/index.html <- copied and modified from frontend/index.html
assets/ <- copied from frontend/public/
```

## 4. Setup frontend
### Install webpack-bundle-tracker
webpack-bundle-tracker alpha version (or greater) required for webpack 4 support
```
cd frontend
npm install --save-dev webpack-bundle-tracker@1.0.0-alpha.0
```
### Create .env file
```
cp .env.sample .env
```

### Modify frontend files to use webpack-loader
Check the pull request for changes in:
```
frontend/config
```

## 5. Run dev server
### Start the npm server
```
cd frontend/
npm start
```
### Start the python server
```
cd ..
./manage.py runserver
```

## Run production build
### Build the frontend bundle
cd frontend/
npm build
### Start the python server with production settings
```
cd ..
./manage.py runserver --settings=backend.settings_production
```
