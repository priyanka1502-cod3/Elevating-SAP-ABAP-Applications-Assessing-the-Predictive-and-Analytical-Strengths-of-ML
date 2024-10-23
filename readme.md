#First Apply the python code using Boston dataset
# Then create an api using pythonanywhere website
Here are steps to deploy your Flask application to 
PythonAnywhere:
Create a PythonAnywhere Account
Go to PythonAnywhere signup page and create a new account.
Upload Your Files
Log in to your PythonAnywhere account and go to "Files" tab.
Upload your Flask application file (e.g., app.py) and any other 
necessary files (like your pickle file).
Set Up Your Web App
Go to "Web" tab and click on "Add a new web app".
Follow prompts to set up your web app. When asked for 
framework, choose "Flask". When asked for Python version, 
choose version you're using. When asked for path to your Flask 
application file, enter path to app.py file you uploaded.
Install Your Dependencies
Go to "Consoles" tab and start a new Bash console.
In console, run pip install flask pandas pickle-mixin to install 
your dependencies.
Reload Your Web App
Go back to "Web" tab and click on "Reload" button to start your 
web app.
After you've set up your web app, PythonAnywhere will provide 
a public URL for accessing your application. You can use this 
URL to call your Python service from your SAP ABAP 
environment.
Please note that PythonAnywhere expects your Flask application 
to be named flask_app.py by default. If your application is named 
app.py, you'll need to specify that when you're setting up your 
web app.
Also, remember to upload your pickle file 
(Random_Forest_model.pkl) to PythonAnywhere using same 
process.
Now that you have your Flask application set up on 
PythonAnywhere, next step is to make sure that your application 
is running correctly.
Check Your Web App's Status
Go to "Web" tab in PythonAnywhere.
Check "Status" section at top of page. It should say "Your web 
app is running".
Visit Your Web App's URL
In "Web" tab, find "link for anonymous access" in "Code" 
section. This is public URL for your web app.
Click on link to visit your web app's URL. You should see 
default page for your Flask application.
Test Your Prediction Endpoint
You can test your prediction endpoint by sending a POST request 
to https://<your-app-name>.pythonanywhere.com/predict, 
replacing <your-app-name> with your PythonAnywhere 
username.
You can use a tool like curl or Postman to send POST request. 
request should include a JSON body with input data for your 
prediction model.
Deploy Flask 
application 
deploy your Flask application on PythonAnywhere, follow these 
steps:
Log in to your PythonAnywhere account and go to "Web" tab.
Click on "Add a new web app" button. Follow prompts to set up 
your web app. When asked for framework, choose "Flask". When 
asked for Python version, choose version you're using. When 
asked for path to your Flask application file, enter path to app.py 
file you uploaded.
Install Your Dependencies
Go to "Consoles" tab and start a new Bash console.
In console, run pip install flask pandas pickle-mixin to install 
your dependencies.
Reload Your Web App
Go back to "Web" tab and click on "Reload" button to start your 
web app.
After you've set up your web app, PythonAnywhere will provide 
a public URL for accessing your application. You can use this 
URL to call your Python service from your SAP ABAP 
environment.
to deploy app.pyon PythonAnywhere, you need to upload app.py 
file to PythonAnywhere. Here's how you can do it:
Download app.py file from Google Colab: After running cell 
with %%writefile app.py, you can download app.py file by 
clicking on folder icon in left sidebar, right-clicking on app.py, 
and selecting "Download".
Upload app.py file to PythonAnywhere: Log in to your 
PythonAnywhere account, go to "Files" tab, click on "Upload a 
file" button, and choose app.py file from your local system.
Reload your web app: Go back to "Web" tab and click on 
"Reload" button.
To run your Flask application on PythonAnywhere, follow these 
steps:
app.py code
Upload your files: Upload your Flask application files (including 
your app.py and any other necessary files like your pickle file) to 
PythonAnywhere. You can do this using "Files" tab on 
PythonAnywhere dashboard.
Set up a new web app: Go to "Web" tab on PythonAnywhere 
dashboard and click on "Add a new web app". Follow steps to set 
up a new web app. When asked for framework, choose "Flask". 
When asked for Python version, choose one that matches your 
application.
Configure web app: After web app is created, you'll be taken to a 
configuration page. In "Source code" section, enter path to your 
app.py file in "WSGI configuration file" field. This tells 
PythonAnywhere where your application is.
Install any necessary packages: If your application requires any 
Python packages that aren't installed by default on 
PythonAnywhere, you can install them using a Bash console. 
You can open a new console from "Consoles" tab. To install 
packages, you can use pip. For example, if you need requests 
package, you can install it with pip install requests.
Reload web app: After you've set up everything, go back to 
"Web" tab and click on "Reload" button. This will start your 
application.
Check your application: You can now check your application by 
visiting your PythonAnywhere URL, which will be something 
like http://<your-username>.pythonanywhere.com.
model = pickle.load(f)
@app.route('/')
def home():
return "Hello, this is my Flask application!"
# Define a new route that will accept POST requests and call 
your prediction function
@app.route('/predict', methods=['POST'])
def predict():
data = request.get_json() # Get input data from POST request
input_data = data['input'] # Extract input data from request
prediction = model.predict(input_data) # Call your prediction 
function
return jsonify(prediction.tolist()) # Return prediction as a JSON 
response
Python script to make a 
POST request
# Run your Flask application
if __name__ == '__main__':
app.run(host='0.0.0.0', port=5000)
import requests
import json
# Replace this with your actual data
data = {
"input": [0.00632, 18.0, 2.31, 0, 0.538, 6.575, 65.2, 4.0900, 1, 
296, 15.3, 396.90, 4.98]
}
response = 
requests.post("http://yourname.pythonanywhere.com/predict", 
data=json.dumps(data))
print(response.json())
Python script that loads 
a pickle file and makes 
a prediction
import pickle
import pandas as pd
# Load model from pickle file
with open('Random_Forest_model.pkl', 'rb') as f:
model = pickle.load(f)
# Create a sample input vector with feature names
input_data = pd.DataFrame([[0.00632, 18.0, 2.31, 0, 0.538, 
6.575, 65.2, 4.0900, 1, 296, 15.3, 396.90, 4.98]],
columns=['CRIM', 'ZN', 'INDUS', 'CHAS', 'NOX', 'RM', 'AGE', 
'DIS', 'RAD', 'TAX', 'PTRATIO', 'B', 'LSTAT'])
# Make a prediction
prediction = model.predict(input_data)
# Print prediction
Final app.py file
# Import necessary libraries
import pickle
from flask import Flask, request, jsonify
import numpy as np # Add this line
# Load pickle file
with 
open('/homeyourwebsitename/mysite/Random_Forest_model.pkl', 
'rb') as f:
 model = pickle.load(f)
model = pickle.load(f)
# Create a new Flask web server
app = Flask(__name__)
@app.route('/')
def home():
return "Hello, this is my Flask application!"
# Define a new route that will accept POST requests and call 
your prediction function
@app.route('/predict', methods=['POST'])
def predict():
data = request.get_json() # Get input data from POST request
input_data = np.array(data['input']).reshape(1, -1) # Reshape data 
to a 2D array
prediction = model.predict(input_data) # Call your prediction 
function
return jsonify(prediction.tolist()) # Return prediction as a JSON 
response
# Run your Flask application
if __name__ == '__main__':
app.run(host='0.0.0.0', port=5000)
# Load model from pickle file
with open('Random_Forest_model.pkl', 'rb') as f:
model = pickle.load(f)
# Create a sample input vector with feature names
input_data = pd.DataFrame([[0.00632, 18.0, 2.31, 0, 0.538, 
6.575, 65.2, 4.0900, 1, 296, 15.3, 396.90, 4.98]],
columns=['CRIM', 'ZN', 'INDUS', 'CHAS', 'NOX', 'RM', 'AGE', 
'DIS', 'RAD', 'TAX', 'PTRATIO', 'B', 'LSTAT'])
# Make a prediction
prediction = model.predict(input_data)
# Print prediction
# Then use the sap hana environment and start righting your abap program

The aim of this project is to develop a prototype application 
that integrates Python and machine learning algorithms with 
SAP ABAP applications. We will be using a housing price 
prediction dataset and machine learning models to predict 
housing prices. The goal is to demonstrate how machine 
learning can be used to enhance the capabilities of SAP ABAP 
applications and to investigate the impact of this integration on 
the overall performance and efficiency of the applications.
Here are the steps on setting up the environment.
Step 1: Install SAP HANA Studio
Download the SAP HANA Studio from the SAP Development 
Tools page.
Extract the downloaded file.
Run the hdbsetup file to start the installation.
Follow the prompts to complete the installation.
Step 2: Set Up ABAP Development Tools
ABAP Development Tools (ADT) are a set of plugins for the 
Eclipse IDE. So, first, you need to install Eclipse. You can 
download it from the Eclipse website.
Once Eclipse is installed, open it and go to "Help" -> "Eclipse 
Marketplace".
In the Eclipse Marketplace dialog, search for "ABAP".
Find "ABAP Development Tools for SAP NetWeaver" and 
click "Go".
Click "Install" to install the ABAP Development Tools.
Step 3: Install Python
Download the latest version of Python from the official 
website.
Run the installer file and follow the prompts to install Python.
Make sure to check the box that says "Add Python to PATH" 
during the installation.
Here's how you can associate a new project with an SAP 
system connection in SAP HANA Studio:
Open SAP HANA Studio: Launch SAP HANA Studio from 
your list of programs.
Create a New System: In the "Systems" view, right-click in the 
white space, and select "Add System".
Enter System Details: In the "Add System" dialog box, you'll 
need to enter the details of your SAP HANA system. For the 
host name, enter the IP address of your system (192.168.7.229). 
For the instance number, enter the instance number of your 
system. The instance number is typically a two-digit number 
that you should have received when your SAP HANA system 
was set up.
Enter SID: In the same dialog box, you'll also need to enter the 
System ID (SID) of your SAP HANA system. In your case, this 
would be "A4H".
Finish the Setup: Click "Next" to proceed through the rest of 
the dialog box. You'll need to enter your user name and 
password for the SAP HANA system, and you might need to 
enter additional details depending on your system's 
configuration. Once you've entered all the necessary details, 
click "Finish" to add the system.
Check the System Connection: After you've added the system, 
it should appear in the "Systems" view in SAP HANA Studio. 
You can expand the system to see its various components (like 
Catalog, Content, Security, etc.). If you're able to see these 
components and interact with them without any errors, this 
means that your system connection is working properly.
the next step is to integrate this model with your SAP ABAP 
application. Here's how you can do it:
Create a Python Script: Write a Python script that can make 
requests to your hosted model. This script should take input 
data, send it to your model, and return the model's predictions. 
You can use the requests library in Python to make HTTP 
requests.
Expose Python Script as a Web Service: Host this Python script 
as a web service. This will allow your ABAP application to 
make HTTP requests to the script. You can use a framework 
like Flask or Django to do this.
Call Web Service from ABAP: Write ABAP code that can 
make HTTP requests to your Python web service. You can use 
the CALL HTTP statement in ABAP to do this. The ABAP 
code should take the necessary input data, send it to the Python 
web service, and handle the returned predictions.
Test the Integration: Test the integration by running your 
ABAP application and checking if the predictions from your 
model are correctly returned and handled.
To write and execute ABAP code, you would typically use the 
ABAP Development Tools (ADT) in Eclipse or the SAP GUI 
with the ABAP editor. Here are the steps to create a new ABAP 
program:
ABAP ADT Using ABAP Development Tools in Eclipse:
Click "Install" to install the ABAP Development Tools.
Step 3: Install Python
Open Eclipse and switch to the ABAP perspective.
In the "Project Explorer" view, navigate to your ABAP project 
and expand it.
Right-click on the "Z-local" package (or the package where you 
want to create your program), select "New" -> "ABAP 
Program".
Enter a name and a description for your program, and click 
"Next".
Select "Executable Program" as the program type, and click 
"Next".
Enter a name for your main program, and click "Finish".
You can now write your ABAP code in the editor that opens.
The project's goal is to develop a prototype application that 
demonstrates the integration of Python and machine learning 
algorithms with SAP ABAP applications. The specific task is to 
implement a housing price prediction model that has been 
trained and hosted on a Python server (pythonanywhere.com). 
The SAP ABAP application will make HTTP requests to this 
Python server to get predictions.
Using SAP HANA Studio
In SAP HANA Studio, you can create and run ABAP programs 
using the ABAP perspective. Here are the steps:
Open SAP HANA Studio and switch to the ABAP perspective.
In the Project Explorer view, navigate to your ABAP project.
Right-click on the project and select New -> Other ABAP 
Repository Object.
In the New ABAP Repository Object wizard, expand the 
Program node, select Program and click Next.
In the Name page, enter a name and description for the program 
and click Next.
In the Template Selection page, select Executable Program and 
click Finish.
In the new program, enter the following code:
CLASS zhousing DEFINITION PUBLIC FINAL CREATE 
PUBLIC.
 PUBLIC SECTION.
 METHODS: predict_housing_price.
ENDCLASS.
CLASS zhousing IMPLEMENTATION.
 METHOD predict_housing_price.
 DATA: url TYPE string,
 http_client TYPE REF TO if_http_client,
 response TYPE string.
 url = 'http://yourname.pythonanywhere.com/predict'. " 
Replace with your actual URL
 CALL METHOD cl_http_client=>create_by_url
 EXPORTING
 url = url
 IMPORTING
 client = http_client
 EXCEPTIONS
 argument_not_found = 1
 plugin_not_active = 2
 internal_error = 3.
 IF sy-subrc <> 0.
 " Handle error
 ENDIF.
 CALL METHOD http_client->send
 EXCEPTIONS
 http_communication_failure = 1
 http_invalid_state = 2.
 IF sy-subrc <> 0.
 " Handle error
 ENDIF.
 CALL METHOD http_client->receive
 EXCEPTIONS
 http_communication_failure = 1
 http_invalid_state = 2
 http_processing_failed = 3.
 IF sy-subrc <> 0.
 " Handle error
 ENDIF.
 response = http_client->response->get_cdata( ).
 WRITE: / 'Response:', response.
 ENDMETHOD.
ENDCLASS.
SAP GUI test
The output of an ABAP program is typically displayed in the 
SAP GUI screen immediately after the program is executed. 
Here's how you can execute the program and view its output:
In the SAP Easy Access screen, enter SE38 in the command 
field and press Enter. This will open the ABAP Editor.
In the ABAP Editor, enter the name of your program 
(ZHOUSING_TEST) in the Program field and click on the 
Execute button (or press F8). This will run the program.
After the program is executed, the output will be displayed in a 
new screen. If your program is working correctly, you should 
see a line that starts with Response: followed by the response 
from the Python server.
Wkg(zhousing_new)
CLASS zhousing DEFINITION PUBLIC FINAL CREATE 
PUBLIC.
 PUBLIC SECTION.
 METHODS: predict_housing_price.
ENDCLASS.
CLASS zhousing IMPLEMENTATION.
 METHOD predict_housing_price.
 DATA: url TYPE string,
 http_client TYPE REF TO if_http_client,
 response TYPE string,
 json_data TYPE string,
 xstring_data TYPE xstring,
 http_request TYPE REF TO if_http_request.
 TRY.
 url = 'http://yourname .pythonanywhere.com/'. " 
Replace with your actual URL
 CALL METHOD cl_http_client=>create_by_url
 EXPORTING
 url = url
 IMPORTING
 client = http_client
 EXCEPTIONS
 argument_not_found = 1
 plugin_not_active = 2
 internal_error = 3.
 IF sy-subrc <> 0.
 " Handle error
 ENDIF.
 " Prepare JSON data
 json_data = '{ "input": [0.00632, 18.0, 2.31, 0, 0.538, 
6.575, 65.2, 4.0900, 1, 296, 15.3, 396.90, 4.98] }'. " Replace 
with your actual data
 " Convert JSON data to xstring
 CALL FUNCTION 'SCMS_STRING_TO_XSTRING'
 EXPORTING
 text = json_data
 mimetype = 'application/json'
 IMPORTING
 buffer = xstring_data.
 http_request = http_client->request.
 " Set the request method and body
 CALL METHOD http_request->set_method
 EXPORTING
 method = if_http_request=>co_request_method_post.
 CALL METHOD http_request->set_header_field
 EXPORTING
 name = 'Content-Type'
 value = 'application/json'.
 CALL METHOD http_request->set_data
 EXPORTING
 data = xstring_data.
 CALL METHOD http_client->send
 EXCEPTIONS
 http_communication_failure = 1
 http_invalid_state = 2.
 IF sy-subrc <> 0.
 " Handle error
 ENDIF.
 CALL METHOD http_client->receive
 EXCEPTIONS
 http_communication_failure = 1
 http_invalid_state = 2
 http_processing_failed = 3.
 IF sy-subrc <> 0.
 " Handle error
 ENDIF.
 response = http_client->response->get_cdata( ).
 DATA: status_code TYPE i,
 status_reason TYPE string.
 CALL METHOD http_client->response->get_status
 IMPORTING
 code = status_code
 reason = status_reason.
 WRITE: / 'Response Code:', status_code.
 WRITE: / 'Response Reason:', status_reason.
 WRITE: / 'Response:', response.
 CATCH cx_root INTO DATA(e_text).
 WRITE: / e_text->get_text( ).
 ENDTRY.
 ENDMETHOD.
ENDCLASS.
Test HTTP connection
Open SAP GUI and login to your SAP system.
In the command field, enter SM59 and press Enter. This will 
open the RFC Destinations screen.
Click on the HTTP Connections to External Server folder.
Click on the Create icon (looks like a piece of paper) to create a 
new HTTP connection.
Fill in the following fields:
RFC Destination: Enter a name for the connection (e.g., 
PYTHONANYWHERE).
Connection Type: Select G for HTTP Connection to External 
Server.
Description: Enter a description for the connection (e.g., 
Connection to PythonAnywhere).
Switch to the Technical Settings tab and fill in the following 
fields:
Target Host: Enter the host name of your Python service (e.g., 
priyanka2023.pythonanywhere.com).
Service No: Enter the port number. If your Python service is 
running on the standard HTTP port, this should be 80. If it's 
running on the standard HTTPS port, this should be 443.
Path Prefix: Enter the path to your Python service (e.g., 
/predict).
Switch to the Logon & Security tab. If your Python service 
requires a username and password, enter them here.
Click on the Save icon to save the connection.
To test the connection, click on the Connection Test button. 
This will send an HTTP request to your Python service and 
display the response.
# Then use PAL for predicting the data and a curve is predicted .

Library Steps
PAL
1. Ensure you have the necessary license for SAP HANA, 
predictive analytics. 2. PAL is included in the SAP HANA 
platform installer. If it's not installed, you might need to 
reinstall SAP HANA with the correct options, or install the 
PAL delivery unit using the SAP HANA Application Lifecycle 
Management (HALM). 3. After installation, enable PAL using 
the SQL command: CALL 
SYS.AFLLANG_WRAPPER_PROCEDURE_CREATE('SYS', 
'AFLPAL', 'lang');
APL
1. Obtain the SAP HANA Automated Predictive Library from 
the SAP Software Download Center. 2. Install the APL on 
your SAP HANA system using the HALM. 3. After 
installation, enable APL using the SQL command: CALL 
SYS.AFLLANG_WRAPPER_PROCEDURE_CREATE('SYS', 
'AFLAPL', 'lang');
EML
1. Ensure you have the necessary license for SAP HANA, 
external machine learning. 2. EML is included in the SAP 
HANA platform installer. If it's not installed, you might need to 
reinstall SAP HANA with the correct options, or install the 
EML delivery unit using the HALM. 3. After installation, 
configure EML to connect to your external machine learning 
server. This involves setting several system parameters and 
possibly adjusting your network settings.
SAP HANA R
1. Install an R server on a machine that can connect to your 
SAP HANA system. 2. Install the necessary R packages on the 
R server. 3. Configure SAP HANA to connect to the R server. 
This involves setting several system parameters and possibly 
adjusting your network settings.
Steps using Pyhbd
pip install pyhdb
import pyhdb
connection = pyhdb.connect(
 host="myhanahost.com",
 port=30015,
 user="myusername",
 password="mypassword"
)
cursor = connection.cursor()
cursor.execute("SELECT * FROM my_table")
results = cursor.fetchall()
cursor.close()
connection.close()
SAP_PAL Code:
PAL Codes 
Create CREATE SCHEMA BostonHousing;
Import CSV Data into a New Table: Importing 
CSV data into a new table in SAP HANA can be 
accomplished via the Import functionality:
Right-click on the newly created schema and 
navigate to Import.
Choose Data From Local File.
Choose your housing.csv file.
In the 'Target Table' section, create a new table 
name (for example, HOUSING_DATA).
Choose First Row Contains Column Names if your 
CSV file contains column names in the first row.
Preview the data if necessary and run the import.
Verify SELECT * FROM 
BostonHousing.HOUSING_DATA;
Check PAL installation SELECT * FROM SYS.AFL_PACKAGES 
WHERE PACKAGE_NAME = 'AFLPAL';
Function header table
Create Tables for PAL
CREATE COLUMN TABLE 
BostonHousing.PAL_LR_FUNCTION_HEADER 
(
POSITION INTEGER,
ARGUMENT_NAME NVARCHAR(100),
DATA_TYPE NVARCHAR(100)
);
Parameter table
CREATE COLUMN TABLE 
BostonHousing.PAL_LR_PARAMETER (
NAME NVARCHAR(100),
INT_VALUE INTEGER,
DOUBLE_VALUE DOUBLE,
STRING_VALUE NVARCHAR(100)
);
Model table
CREATE COLUMN TABLE 
BostonHousing.PAL_LR_MODEL (
ROW_INDEX INTEGER,
COEFFICIENT DOUBLE,
STANDARD_ERROR DOUBLE,
T_STAT DOUBLE,
P_VALUE DOUBLE
);
Summary table
CREATE COLUMN TABLE 
BostonHousing.PAL_LR_SUMMARY (
STAT_NAME NVARCHAR(60),
STAT_VALUE DOUBLE
);
Insert Data into PAL Tables Insert into Function header table
INSERT INTO 
BostonHousing.PAL_LR_FUNCTION_HEADER 
VALUES (1, 'DEPENDENT', 'DOUBLE');
INSERT INTO 
BostonHousing.PAL_LR_FUNCTION_HEADER 
VALUES (2, 'INDEPENDENT', 'DOUBLE');
Insert into Parameter table
INSERT INTO 
BostonHousing.PAL_LR_PARAMETER 
VALUES ('THREAD_NUMBER', 2, NULL, 
NULL);
Call PAL Function
This will train a linear regression model on the 
HOUSING_DATA table, using all columns except 
MEDV as independent variables and MEDV as the 
dependent variable.
Call PAL Function CALL 
_SYS_AFL.PAL_LINEAR_REGRESSION(
BostonHousing.HOUSING_DATA,
BostonHousing.PAL_LR_FUNCTION_HEADER,
BostonHousing.PAL_LR_PARAMETER,
BostonHousing.PAL_LR_MODEL,
BostonHousing.PAL_LR_SUMMARY
) WITH OVERVIEW;
After this step, the PAL_LR_MODEL table will 
contain the coefficients of the linear regression 
model, and the PAL_LR_SUMMARY table will 
contain summary statistics about the model.
second step: 
setting up the SAP system to send HTTP requests 
to your Python server. This involves using ABAP 
programming to send HTTP requests and process 
the responses.
Open SAP HANA Studio: Start the SAP HANA 
Studio application on your computer.
Navigate to ABAP Perspective: If not already in 
the ABAP perspective, you can switch to it by 
going to Window > Perspective > Open 
Perspective > ABAP.
Create New ABAP Program: In the Project 
Explorer pane, navigate to your desired package 
(you might need to log in to the SAP system if not 
already done). Right-click the package, go to New 
> Other ABAP Repository Object. A dialog box 
will appear. Navigate to ABAP Program and click 
Next.
Provide Details: Enter a Name and Description for 
the new program. The name should be in 
uppercase and follow your company's naming 
conventions for ABAP programs. Click Next and 
then Finish.
Write the ABAP Code: You should now see a 
new, blank ABAP program. Here, you can write 
the ABAP code as mentioned in the previous 
response.
Save and Activate: After writing the code, save the 
program by clicking the Save button (floppy disk 
icon), and then activate it by clicking the Activate
button (checkmark icon).
Run the Program: You can now run the program 
by pressing the F8 key. If the program runs 
without errors, it will send the HTTP request to 
your Python server and process the response.
Codes
DATA: http_client TYPE REF TO if_http_client,
http_request TYPE REF TO if_http_request,
http_response TYPE REF TO if_http_response,
json_string TYPE string,
json_parser TYPE REF TO cl_sxml_json_parser,
response_data TYPE REF TO data.
TRY.
" Create HTTP client
CALL METHOD cl_http_client=>create_by_url
EXPORTING
url = 
'http://priyanka2023.pythonanywhere.com/predict' 
" Replace with your Python server URL
IMPORTING
client = http_client
EXCEPTIONS
argument_not_found = 1
plugin_not_active = 2
internal_error = 3.
" Get HTTP request
http_request = http_client->request.
" Set request method and header fields
http_request->set_method( 'POST' ).
http_request->set_header_field( name = 'Content￾Type'
value = 'application/json' ).
" Set request body with your input data
json_string = '{ "input": [0.00632, 18.0, 2.31, 0, 
0.538, 6.575, 65.2, 4.0900, 1, 296, 15.3, 396.90, 
4.98] }'.
http_request->set_data( data = json_string ).
" Send HTTP request
http_client->send( ).
" Receive HTTP response
http_client->receive( ).
" Get HTTP response
http_response = http_client->response.
Parse JSON response 
DATA: response_data TYPE string. 
CALL TRANSFORMATION id SOURCE XML 
http_response->get_data( ) 
 RESULT response_data = 
response_data.
json_parser = cl_sxml_json_parser=>create( data 
= http_response->get_data( ) ).
response_data = json_parser->get_data( ).
" Now response_data contains the parsed JSON 
response
CATCH cx_root INTO DATA(e_text).
WRITE: / 'Error:', e_text->get_text( ).
ENDTRY.
