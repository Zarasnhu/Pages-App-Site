# Pages-App-Code
This repository is for, Assignment: Pages App Code 
import os
from flask import Flask
from dotenv import load_dotenv
import psycopg2

load_dotenv()

app = Flask(__name__)

DATABASE_URL = os.getenv("DATABASE_URL", "postgresql://postgres:password@localhost:5432/my_database")

def get_db_connection():
    """
    Establish a connection to the PostgreSQL database.
    """
    try:
        conn = psycopg2.connect(DATABASE_URL)
        print("Database connected successfully!")
        return conn
    except Exception as e:
        print(f"Error connecting to the database: {e}")
        return None

@app.route("/")
def home():
    """
    Home route to test the database connection.
    """
    conn = get_db_connection()
    if conn:
        conn.close()
        return "Hello, World! Connected to the database successfully!"
    else:
        return "Hello, World! Failed to connect to the database."

if __name__ == "__main__":
    # Run the Flask app
    app.run(debug=True)

