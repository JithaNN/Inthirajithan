
# Student CV Management Portal
One of our clients from a higher education institute has requested us to implement a Student CV Management Portal for their students so that students can maintain a profile with their details and CV. And the companies are able to go through the CVs and select candidates they want. Therefore this system has 3 users.

-  **Admin** : Admin has the capability of adding companies. And also to approve added CVs.
-  **Student** : Students can be added to the system and their CV approvals are shown in the frontend.
-  **Company** : Companies can access the system with the account which the admin has provided them and select candidates which they wish to interview.

Our software engineers have planned the architecture and started implementing the system which has been provided in this repository. Your task is to complete following tasks and fix the bugs which are failing the test cases in the given time. Test cases have already been written for the features to be implemented so that you can make sure you have implemented the required features properly. Before working on anything, the team wants you to run the tests and see where the application is breaking. You can refer the instructions below to run the tests.

## Instructions to setup & run the project

### Tools Required
- XAMPP or a local server application to run the backend
  XAMPP Download link : https://www.apachefriends.org/xampp-files/7.4.14/xampp-windows-x64-7.4.14-0-VC15-installer.exe
- Use SQLite DB Browser or a Database management application to view the database.
- Composer - https://getcomposer.org/download/

### Important Notes
- A restart may be requried to run the above tools properly
- Solution for `php is not recognized as an internal or external command`, use command: `SET PATH=%PATH%;C:\xampp\php`
- Rename the `env` and the `env.testing` file to `.env` and `.env.testing` located in the `backend` folder

### To run the back end application
- `cd backend`
- `composer install`
- `php artisan key:generate`
- `php artisan serve`

#### Tips
- Database file can be found in `backend/storage/database.sqlite`

## Running test cases

#### Front-End
- Install [jestjs](https://jestjs.io/docs/en/getting-started) CLI as its used for running tests in this template.
- Execute below statements in a terminal
- Install project dependencies: ```npm install```

Run tests:
- ```npm install -g jest```
- ```cd frontend```
- ```jest```

#### Back-End
- ```cd backend```
- ```php artisan test```

## Evaluation
Evaluation will be based on results of test cases. **So make sure to run the test cases before pushing the code.**

## Bugs
#### Back-End

1. When we request to reject the student CV, it doesn't reject the CV.

	##### Expected Behaviour

	- When the function is called, the CV of the student should be rejected so that for the given student `isCvApproved = 0`

	##### Current Behaviour

	- When we call the function to reject the CV of the Student, it will be called but it does not update the students table.

2.  When a user tries to add a company into the database, the  data is not added into the database.  

	Hint: check  `companyName`

    ##### Expected Behaviour

	- companyName, username and password  fields should be required when storing data in the database.

    ##### Current Behaviour

	- when a user tries to add a company into the database, the  data is not added into the database and it gives an error.  
	

3. The user information is not returned back to the client when the `user/{id}` endpoint is called.
	##### Expected Behaviour
    - The user object should be returned from the endpoint back to the client 
    
    ##### Current Behaviour
    - The  `user` object is retrieved from the database, but it is not returned back to the client as the currently returned value is `null` from the endpoint

#### Front-End

1.  Change the browser title and page heading from "Student Management App" to "Student CV Management Portal"

    ##### Expected Behaviour
    - Application & Browser Tab Name should be "Student CV Management Portal"
    ##### Current Behaviour
    - Application & Browser Tab Name is "Student Management App"
    
2. Change the "Add Company" button text to "Submit"
    ##### Expected Behaviour
    - Button text should be "Submit"
    ##### Current Behaviour
    - Button text is "Add Company"

3. Change the button color in the "Add Company" section to Green via inline styling
    ##### Expected Behaviour
    - Button color should be Green.
    ##### Current Behaviour
    - No button color is present

## Features Required
#### Back-End
1. `getAllStudents()` should be implemented in the `StudentController` to retrive all the information of the students in the table `students` using the model class `Student` 
Sample output:-
    ```
    "message": [
        {
            "index": "1",
            "name": "dave",
            "email": "dave@gmail.com",
            "degreeType": "BSC Hons",
            "available": "1",
            "gpa": "3.1",
            "year": "2002",
            "isCvApproved": "0",
            "gender": "Male",
            "positionList": "[Test,Test]"
        },
        {
            "index": "2",
            "name": "jakob",
            "email": "jakob@gmail.com",
            "degreeType": "BSC in SE",
            "available": "0",
            "gpa": "3.5",
            "year": "2010",
            "isCvApproved": "0",
            "gender": "Male",
            "positionList": "[BA,SE]"
        },
        {
            "index": "3",
            "name": "mike",
            "email": "mike@gmail.com",
            "degreeType": "BSC in IBM",
            "available": "0",
            "gpa": "3.8",
            "year": "2015",
            "isCvApproved": "0",
            "gender": "Male",
            "positionList": "[BA,QA,SSE]"
        }
    ]
    ```
2. Create Library - `Idlib` and create the function `generate()`.
It is required to generate a `base 64 encoded ID` when adding companies. The ID should contain the following attributes.

    **For Company**
        - Prefix - "DG"
        - CompanyName
        - CurrentTimestamp
        - Format : Prefix_CompanyName_CurrentTimestamp

3. `getStudentById()` should be implemented in the `StudentController` to retrive the information of a student in the table `students` using the model class `Student` with the given `index`. 
Sample output:-
    ```
     "message": {
        "index": "1",
        "name": "dave",
        "email": "dave@gmail.com",
        "degreeType": "BSC Hons",
        "available": "1",
        "gpa": "3.1",
        "year": "2002",
        "isCvApproved": "0",
        "gender": "Male",
        "positionList": "[Test,Test]"
    }
    ```
4. `approveCVForId()` should be implemented in the `StudentController` to approve the CV of a student in the table `students` for the the given `index`. 
Sample output:-
    ```
    {
        "message": "Approved Successfully!"
    }
    ```
#### Front-End

1.  "Clear" button implementation in "View Student Information" section
    - When the user clicks on the "Clear" button the paragraph section below should display the text "Student Information Will Be Displayed Here" and the input field for the Student Index should be cleared.

2. Search Button Disabled till Search Input Is Given
    - Until the Student Index has been entered, the "Search" button must remain disabled. **(hint-use keyup event)**

3. Construct a  `regular expression` to ensure that the client can enter an input for the field with `id="company-password"` that has **only 6 alpha-numeric characters**
    - Example: The input `1AB2c3` should be allowed to be entered but an input such as `!Aasd@asd` should be blocked. (hint - use the `pattern` attribute of the input element)
4. Construct a  `regular expression` to ensure that the client can enter an input for the field with `id="student-id"` that accepts **only digits**  
    - Example: The input `1AB2c3` should **not** be allowed to be entered but an input such as `123456` should be blocked. (hint - use the `pattern` attribute of the input element)

## Assignment Time: 4 hours
