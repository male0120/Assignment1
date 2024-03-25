Assignment 1

This assignment seeks to create a robust monitoring solution for an application deployed on Kubernetes, integrating Single Sign-On (SSO) via Gmail for user authentication. The system retrieves application events through a syslog server and forwards the data to Azure Log Analytics for analysis. Grafana is then employed to visualize telemetry data from Azure Log Analytics, offering valuable insights into the application's performance and usage trends.

Group Members: Parvezbhai Malek, Yash Solanki, Thep Rungpholsatit
PRESENTED TO: ISLAM GOMAA

1.	Deployment of Web-APP Google SSO Pod


Firstly, we created a simple web application using python:

app.py:

This code is a Flask application that implements OAuth2 authentication with Google using the requests_oauthlib library. Let's break down the key components:

Flask Setup:

The Flask application is created and initialized.
A secret key is generated for session management.

OAuth Configuration:

•	CLIENT_ID, CLIENT_SECRET, and REDIRECT_URI are provided by Google when you register your application with the Google API Console.
•	SCOPE specifies the permissions that the application requests from the user.
•	AUTHORIZATION_BASE_URL is the URL where the user is redirected to authorize the application.
•	TOKEN_URL is the URL used to exchange the authorization code for an access token.

Routes:

/: Redirects to the login route.
/login: Initiates the OAuth2 authentication process by redirecting the user to Google's authorization URL.
/login/callback: Handles the callback from Google after the user authorizes the application.

OAuth Flow:
•	When a user visits /login, they are redirected to Google's authorization URL, where they can log in and grant permissions to the application.
•	After authorization, the user is redirected back to /login/callback.
•	In the callback route, the code checks if the state parameter matches the one stored in the session to prevent CSRF attacks.
•	It then creates an OAuth2Session instance with the client ID, redirect URI, and state retrieved from the session.
•	Using the authorization response received in the callback, it exchanges the authorization code for an access token.
•	With the access token, it fetches the user's information from Google's user info endpoint.
Finally, it returns a message indicating successful authentication along with the user's information.

Main Execution:

•	If the script is executed directly, the Flask application runs in debug mode with SSL enabled using an ad-hoc SSL context.
•	This code provides a basic foundation for implementing OAuth2 authentication with Google in a Flask application. It handles the authentication flow and retrieves user information after successful authorization
![image](https://github.com/male0120/Assignment1/assets/157184498/9bede7a2-1d6c-47a8-9596-a6ed67bee854)
Login.html:

his HTML code provides a simple interface for users to initiate the login process using their Google account. Upon clicking the "Login with Google" link, the user is redirected to the appropriate route in the web application to handle the authentication flow.
![image](https://github.com/male0120/Assignment1/assets/157184498/0f7de74f-9c01-4129-9268-aefa6b350a42)
•	We use OAuth for Authentication:
![image](https://github.com/male0120/Assignment1/assets/157184498/92a5e013-4dea-4f8b-b2ed-fe6a21e2f960)
Output:
![image](https://github.com/male0120/Assignment1/assets/157184498/24bc3cb9-3bf9-4dae-a1c0-7c4ea09e4373)
Authentication Successful:
Localhost: https://127.0.0.1:5000
![image](https://github.com/male0120/Assignment1/assets/157184498/1ab1f92a-d914-4517-bdd5-fef1f8417c2e)
Build Dockerfile:
![image](https://github.com/male0120/Assignment1/assets/157184498/57e83386-c32a-4684-9dba-8ce9b2613686)
1.	Deploying application on Kubernetes:

•	Within its architecture, the Kubernetes cluster hosts a variety of applications and services, acting as the fundamental infrastructure. It is made up of several pods that can communicate with one another to provide an integrated environment for the hosted applications. Kubernetes Services, which guarantee smooth connectivity between the pods and with outside networks, enable networking inside this cluster and allow it to reach outside its internal boundaries. 
•	Azure Monitoring is used for cluster monitoring and performance analysis. This tool, which offers insights into the cluster's performance and health data, is essential to guaranteeing its proper operation. 
Deployment.yaml:
![image](https://github.com/male0120/Assignment1/assets/157184498/3814af1f-f991-4de1-a6a4-e992a75fc036)
Kubectl get svc:
![image](https://github.com/male0120/Assignment1/assets/157184498/7de6ac9a-8d64-4694-b980-7acef2572df7)




