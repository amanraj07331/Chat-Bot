# Nom-Nom Bot: A Food Ordering Chatbot
Nom-Nom Bot is a conversational AI chatbot designed for a fictional restaurant, "Pandeyji Eatery." It allows users to place food orders, add or remove items from an ongoing order, and track the status of their orders through a natural language interface. The project uses Google Dialogflow ES for Natural Language Understanding (NLU) and a Python backend with FastAPI for fulfillment logic and database management.

## Features
Place a New Order: Initiate a new food order.
Add/Remove Items: Modify an ongoing order by adding or removing food items and specifying quantities.
Complete Order: Finalize the order, which is then saved to a database.
Get Order ID: Receive a unique order ID upon completion.
Track Order Status: Check the current status of a previously placed order using the order ID.
Contextual Conversation: Maintains the context of an ongoing order, allowing for a multi-turn conversation.
## Tech Stack
Conversational AI: Google Dialogflow ES
Backend Framework: FastAPI
Database: MySQL
Programming Language: Python
Core Python Libraries: mysql-connector-python, fastapi, uvicorn

## File Structure
```
.
├── main.py                 # Main FastAPI application file, handles webhook requests from Dialogflow.
├── db_helper.py            # Contains all functions for interacting with the MySQL database.
├── generic_helper.py       # Utility functions, e.g., for parsing session IDs.
├── requirements.txt        # Lists all the Python dependencies for the project.
└── eatery_database.sql     # SQL dump file to set up the database schema and initial data.
```
# Getting Started: Local Setup and Installation
Follow these steps to set up and run the project on your local machine.

**1. Prerequisites**
Python 3.8+: Make sure you have Python installed.

MySQL Server: A running instance of MySQL server. You can use tools like MySQL Community Server with MySQL Workbench.

ngrok: A tool to expose your local server to the internet so Dialogflow can send webhook requests to it.

**2. Database Setup**
    **1. Create the Database:** Open your MySQL client (like MySQL Workbench) and create a new database.
          ```
             CREATE DATABASE pandeyji_eatery;
             ```
    **2. Import the Schema:** Execute the pandeyji_eatery.sql file in your new database. This will create               the necessary tables (food_items, orders, order_tracking) and stored procedures.
    
**3. Backend Server Setup**
      **1. Clone the Repository:
           ```
           git clone <your-repository-url>
           cd <repository-folder>
          ```   
      **2. Create a Virtual Environment (Recommended):**
           ```
              python -m venv venv
              source venv/bin/activate  # On Windows: venv\Scripts\activate
                   ```
      **3. Install Dependencies:**
         ```
          pip install -r requirements.txt
             ```
       **4.Configure Database Connection:**
            Open the db_helper.py file.
            Update the mysql.connector.connect() details with your MySQL username and password.

    cnx = mysql.connector.connect(
           host="localhost",
           user="your_mysql_user",      # e.g., 'root'
           password="your_mysql_password",
           database="pandeyji_eatery"
    )
  **4. Running the Project**
     **1.Start the Backend Server:**
       ```
       uvicorn main:app --reload
       ```
      Your server will be running at http://127.0.0.1:8000.
     **2.Expose Local Server with ngrok:**
       Open a new terminal window.
       Run the following command:

        ngrok http 8000
  ngrok will provide a public HTTPS forwarding URL (e.g., https://xxxx-xx-xx-xx.ngrok.io). Copy this URL.
    
**5. Dialogflow Agent Setup**
  **1.Create a Dialogflow Agent:** Go to the Dialogflow ES Console and create a new agent.

  **2.Import Intents:** Manually create the intents (new.order, order.add, order.remove, order.complete, track.order) and their training phrases as per your project's design.

 **3.Create Entities:** Create a custom entity named @food-item and populate it with the names of the food items from your food_items database table (e.g., "Pizza", "Samosa").

 **4.Configure Fulfillment:**
 In your Dialogflow agent, go to the Fulfillment section.
   Enable the Webhook.
  In the URL field, paste the HTTPS URL you copied from ngrok.
  
**click Save**

  **5.Enable Webhook for Intents:** For each intent that requires backend logic (order.add, order.remove, order.complete, track.order), scroll down to the Fulfillment section within the intent and toggle on "Enable webhook call for this intent".

  ## Sample Output
  ![Alt text for your image](https://github.com/amanraj07331/Chat-Bot/blob/main/Screenshot%202025-07-27%20203455.png)
          
          
    
