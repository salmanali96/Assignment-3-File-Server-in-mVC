# Assignment-3-File-Server-in-mVC




Introduction:
In this assignment I implemented a mechanism for uploading files into Database using Spring MVC 4, Hibernate & MySQL Database. 

Learning Outcomes:
Structure of preparing model classes, dao and service layers
Experience of working in MVC framework
Working in Hibernate and Spring MVC
Methods of preparing Spring Configuration files
Configuring server for running the application
Procedure:
Creating Database:
I implemented user and document relationship. A user can have several documents, it's OneToMany relationship between Users and documents.

create table APP_USER (
   id BIGINT NOT NULL AUTO_INCREMENT,
   sso_id VARCHAR(30) NOT NULL,
   first_name VARCHAR(30) NOT NULL,
   last_name  VARCHAR(30) NOT NULL,
   email VARCHAR(30) NOT NULL,
   PRIMARY KEY (id),
   UNIQUE (sso_id)
);
  
  
create table USER_DOCUMENT(
   id BIGINT NOT NULL AUTO_INCREMENT,
   user_id BIGINT NOT NULL,
   name  VARCHAR(100) NOT NULL,
   description VARCHAR(255) ,
   type VARCHAR(100) NOT NULL,
   content longblob NOT NULL,
   PRIMARY KEY (id),
   CONSTRAINT document_user FOREIGN KEY (user_id) REFERENCES APP_USER (id) ON UPDATE CASCADE ON DELETE CASCADE
);

content longblob will be used to store our file. We will store the files into binary format in this column.
Model Classes:
We created Model Classes in the next step
User_Document was mapped to UserDocument Class
APP_USER is mapped to User class
Dao Layer and Service Layer:
We created userdocument dao and UserDao	
We then created the service layer to define and implement all the functionalities of Dao Layer
Prepare Configuration for File Upload
Spring provides several possibilities to upload a file. We will use one of possible way, which is Programmatic registration of Servlet 3.0 specific javax.servlet.MultipartConfigElement with SpringMVC DispatcherServlet. This registration provides opportunity to set specific properties like maximum file size, request size, location and threshold after which file will be stored temporarily on disk during upload operation.
Additionally, we need to add StandardServletMultipartResolver Bean to our Spring Configuration. It’s a standard implementation of the MultipartResolver interface, based on the Servlet 3.0 javax.servlet.http.Part API.
Create Wrapper class for File
Spring provides org.springframework.web.multipart.MultipartFile which is a representation of an uploaded file received in a multipart request. It provides handy methods like getName(), getContentType(), getBytes(), getInputStream() etc.. which make life bit easier while retrieving information about file being uploaded.
Spring MVC Contoller Class:
The main methods are uploadDocument, downloadDocument and deleteDocument
Other methods include save/update/deleteing a user and basic navigation
Creating a Validator:
A validator file was created to validate file input
Files for Views:
There are several views in this application which were implemented using several JSPs file and styling was done by using CSS and bootstrap

Running the Application:
Load the project into netbeans
Now build the war 
 Deploy the war to a Servlet 3.0 container .
 In case Tomcat, i will simply put this war file into tomcat webapps folder and click on start.bat inside tomcat/bin directory.




