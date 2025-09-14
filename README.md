# Jenkins CI/CD Pipeline with Flask & Docker 🐳

This project demonstrates how to build a CI/CD pipeline using Jenkins for a simple Flask web application, containerized with Docker and orchestrated with Docker Compose.

---

### 🚀 Features

* **Flask App** → A simple Python web app returning "Hello from Flask Jenkins Pipeline!"
* **CI/CD with Jenkins** → Automated build, test, and deployment pipeline
* **Dockerfile** → Containerizes the Flask app for portability
* **docker-compose.yml** → Runs the app in a container, exposed on port 5000
* **Unit Testing** → Includes pytest test cases (`test_app.py`)

---

### 🛠️ Tech Stack

* **Language:** Python (Flask)
* **CI/CD:** Jenkins
* **Containerization:** Docker, Docker Compose
* **Testing:** Pytest

---

### ⚙️ Setup Instructions

1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/ajithsunkara96/jenkins-flask-cicd.git](https://github.com/ajithsunkara96/jenkins-flask-cicd.git)
    cd jenkins-flask-cicd
    ```

2.  **Build & Run with Docker Compose**
    ```bash
    docker-compose up --build
    ```
    App will be available at 👉 `http://localhost:5000`

3.  **Running Tests**
    ```bash
    pytest test_app.py
    ```

---

### 🔄 Jenkins Pipeline

The `Jenkinsfile` defines stages for:

* **Checkout** → Pulls source code from GitHub
* **Build** → Builds Docker image of the Flask app
* **Test** → Runs pytest unit tests
* **Deploy** → Deploys container using Docker Compose

---

### 📚 Learning Outcome

This project demonstrates how to:

* Build a CI/CD pipeline with Jenkins
* Automate testing and deployment of a Flask application
* Use Docker & Docker Compose for containerized development
* Integrate GitHub + Jenkins for continuous integration

---

✍️ **Author:** Venkata Ajith Sunkara
