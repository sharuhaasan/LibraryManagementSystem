# LibraryManagementSystem
Project name - LibraryManagement                                                               
Books - This Django app provides a REST API for managing User and Books in the LibraryManaging system.

### INSTALLATION
#### Clone the repository:
```bash
https://github.com/sharuhaasan/LibraryManagementSystem.git        
```
#### Navigate to the project directory:
```bash
cd LibraryManagement
```                               
#### Create a virtual environment:
```bash
python3 -m venv venv 
```                           
#### Activate the virtual environment:
```bash 
venv\Scripts\activate  
```                                
#### Install the dependencies:  
```bash
pip install -r requirements.txt
```                                  

#### Set up the database:
```bash
python manage.py makemigrations
python manage.py migrate
```
#### DATABASE - PostgreSQL

#### USAGE

settings.py                                   
models.py                                 
serializers.py                              
views.py                                                      
urls.py (Books)                                          
urls.py (LibraryManagement)                  
tests.py

##### Start the development server
```bash
python manage.py runserver
```

### Access the API endpoints:

#### User Authentication
- **Get Access Token:** `POST /api/token/`
- **Refresh Expiring Access Token:** `POST /api/token/refresh/`

#### Users
- **Create New user:** `POST /users/`
- **List All users:** `GET /users/all/`
- **Retrieve details of a specific user by UserID:** `GET /users/<int:UserID>/`
#### Books
- **Create New book:** `POST /books/`
- **List All books:** `GET /books/all/`
- **Retrieve details of a specific book by BookID:** `GET /books/<int:BookID>/`
- **Assign/Update book details:** `PUT /books/details/<int:Book_id>/`
#### Borrowing Books
- **Borrow a book:** `POST /borrow/`
- **(Update) Return a borrowed book:** `PUT /return/<int:pk>/`
- **List All borrowed books:** `GET /borrowed-books/`

### How to get Token 
- http://127.0.0.1:8000/api/token/ -- (POST) Request - `Give Active Username and password`
- **After Successful Authentication** - `Generates "refresh" and "access" token`
#### Token expired
- **Login Again** - http://127.0.0.1:8000/api/token/ -- (POST) Request - `Give Active Username and password`
- **OR**
- http://127.0.0.1:8000/api/token/refresh/  -- (POST) Request - `Give "refresh" token`
- **After Validation** - `Generates new "access" token`

**NO Existing User Account:** Create New User Account
```bash
python manage.py createsuperuser
```
### APIs Security

- **Added `IsAuthenticated` Function to all the API Endpoints** - *This ensures that only authenticated users can access the endpoints*                 

**Postman - API development tool**
- **Add "access" Token in headers section** - *While performing CRUD operations*
- **In Headers, Add `Key = Authorization` and `Value = Bearer Your_access_token`** 

##### AUTHENTICATION ERROR
```bash
If a user attempts to access the API endponits without "access" token in headers/Authorization section, the response will be:

"GET /users/6/ HTTP/1.1" 401 Unauthorized

{
    "detail": "Authentication credentials were not provided."
}
```
##### SAMPLE API

http://127.0.0.1:8000/users/ -- (POST) To create new user                                             
http://127.0.0.1:8000/books/all/ -- (GET) Lists all existing books                                                           
http://127.0.0.1:8000/books/1/ -- (GET) To retrieve the details of existing book using BookID                                                   
http://127.0.0.1:8000/return/5/ -- (PUT) To Update the return date of borrowed book using Primary key                                            

##### RESPONSE
```bash
"POST /users/ HTTP/1.1" 201 Created                                                            
"GET /books/all/ HTTP/1.1" 200 OK                                       
"GET /books/1/ HTTP/1.1" 200 OK                      
"PUT /return/5/ HTTP/1.1" 200 OK          
```
##### TESTING
```bash
python manage.py test 
```
##### TESTING RESULTS
```bash
----------------------------------------------------------------------
Ran 9 tests in 1.288s

OK
```
##### ERROR
```bash
If a user attempts to have another account using same mail id, the response will be:                                          

"POST /users/ HTTP/1.1" 400 Bad Request

{
    "Email": [
        "user with this Email already exists."
    ]
}
```