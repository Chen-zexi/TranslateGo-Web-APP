# TranslateGo

## Product vision statement

An AI powered translation application that helps users quickly look up words, accurately translate text between multiple languages, save translations for future reference, and customize their experience based on specialized topics of interest.


## Steps necessary to run the software

### Method 1: Docker Setup (Recommended)

1. **Prerequisites**
   - Docker and Docker Compose (either as `docker-compose` or the newer `docker compose`)
   - Git
   - Google Gemini API key

2. **Clone the repository**
   ```bash
   git clone https://github.com/software-students-spring2025/2-web-app-many-people
   ```

3. **Configure environment variables**
   - Create a `.env` file in the project root with the following content:
     ```
     FLASK_APP=app
     FLASK_ENV=development
     FLASK_DEBUG=1
     FLASK_PORT=5001
     
     # MongoDB Configuration for local Docker instance
     MONGO_URI=mongodb://admin:secret@mongodb:27017/admin?authSource=admin&authMechanism=SCRAM-SHA-1
     MONGO_DBNAME=translatego_db
     
     # Flask Secret Key (for session security)
     SECRET_KEY=your_secret_key_here
     
     # API Keys for Translation Services
     GEMINI_API_KEY=your_gemini_api_key_here
     ```

4. **Check for port conflicts**
   - The default configuration uses port 5001 for the web app and 27017 for MongoDB
   - If you already have services using these ports, modify the `docker-compose.yml` file to use different ports, for example:
     ```yaml
     # For MongoDB port conflict
     ports:
       - "27018:27017"  # Maps container's 27017 to host's 27018
     
     # For web app port conflict
     ports:
       - "5002:5001"    # Maps container's 5001 to host's 5002
     ```

5. **Build and start the Docker containers**
   ```bash
   docker compose up -d
   ```
   Note: Use `docker-compose up -d` if you have the older Docker Compose installation.

6. **Verify the containers are running**
   ```bash
   docker ps | grep 'translatego\|mongodb'
   ```

7. **Access the application**
   - Open your browser and navigate to `http://localhost:5001` (or the alternative port if you changed it)
   - The application is now running with a MongoDB database in Docker containers

8. **Troubleshooting**
   - If you encounter authentication errors with MongoDB, check that your .env file has the correct MongoDB URI
   - If you see dependency conflicts, you may need to rebuild the containers:
     ```bash
     docker compose down && docker compose up -d --build
     ```

9. **Stop the containers when done**
   ```bash
   docker compose down
   ```

### Method 2: Standard Setup

1. **Prerequisites**
   - Python 3.8 or higher
   - MongoDB (local installation or MongoDB Atlas account)
   - Google Gemini API key

2. **Clone the repository**
   ```bash
   git clone https://github.com/software-students-spring2025/2-web-app-many-people
   ```

3. **Set up a virtual environment**
   ```bash
   python -m venv venv
   
   # On Windows
   venv\Scripts\activate
   
   # On macOS/Linux
   source venv/bin/activate
   ```

4. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

5. **Configure environment variables**
   - Create a `.env` file in the project root
   - Add the following variables (see `env.example` for reference):
     ```
     FLASK_APP=app
     FLASK_ENV=development
     FLASK_DEBUG=1
     FLASK_PORT=5001
     
     # MongoDB Configuration
     MONGO_URI=mongodb://admin:secret@mongodb:27017/admin?authSource=admin&authMechanism=SCRAM-SHA-1
     MONGO_DBNAME=translatego_db
     
     # Flask Secret Key
     SECRET_KEY=your_secret_key_here
     
     # API Keys for Translation Services
     GEMINI_API_KEY=your_gemini_api_key_here
     ```

6. **Run the application**
   ```bash
   python run.py
   ```

7. **Access the application**
   - Open your browser and navigate to `http://localhost:5001`


## Task boards

[Task Boad](https://github.com/orgs/software-students-spring2025/projects/142/views/1)


## Contributors
- [Alan Chen](https://github.com/Chen-zexi)
