# FastAPI Beyond CRUD 

This is the source code for the [FastAPI Beyond CRUD](https://youtube.com/playlist?list=PLEt8Tae2spYnHy378vMlPH--87cfeh33P&si=rl-08ktaRjcm2aIQ) course. The course focuses on FastAPI development concepts that go beyond the basic CRUD operations.

For more details, visit the project's [website](https://jod35.github.io/fastapi-beyond-crud-docs/site/).

## Table of Contents

1. [Getting Started](#getting-started)
2. [Prerequisites](#prerequisites)
3. [Project Setup](#project-setup)
4. [Running the Application](#running-the-application)
5. [Running Tests](#running-tests)
6. [Contributing](#contributing)

## Getting Started
Follow the instructions below to set up and run your FastAPI project.

### Prerequisites
Ensure you have the following installed:

- Python >= 3.10
- PostgreSQL
- Redis

### Project Setup
1. Clone the project repository:
    ```bash
    git clone https://github.com/jod35/fastapi-beyond-CRUD.git
    ```
   
2. Navigate to the project directory:
    ```bash
    cd fastapi-beyond-CRUD/
    ```

3. Create and activate a virtual environment:
    ```bash
    python3 -m venv env
    source env/bin/activate
    ```

4. Install the required dependencies:
    ```bash
    pip install -r requirements.txt
    ```

5. Set up environment variables by copying the example configuration:
    ```bash
    cp .env.example .env
    ```

6. Run database migrations to initialize the database schema:
    ```bash
    alembic upgrade head
    ```

7. Open a new terminal and ensure your virtual environment is active. Start the Celery worker (Linux/Unix shell):
    ```bash
    sh runworker.sh
    ```

## Running the Application
Start the application:

```bash
fastapi dev src/
```
Alternatively, you can run the application using Docker:
```bash
docker compose up -d
```
## Running Tests
Run the tests using this command
```bash
pytest
```

# Continuous Integration Workflows:

## Overview
This repository includes two GitHub Actions workflows:
1. **Conventional Commit Check**: Ensures that all pull request commits follow the [SemVer Conventional Commit](https://www.conventionalcommits.org/) standard.
2. **Nightly Build**: Runs a scheduled nightly build (12am) that tests, builds, and pushes a Docker image. 

---

## 1. Conventional Commit Check
### **Triggers**:
- Runs automatically on **pull requests** targeting the `main` branch.

### **Job: `commit-check`**
- Checks out the PR branch.
- Runs a commit-check action to validate commit messages against the conventional commit standard.
- Adds PR comments if the commit messages do not comply.

### **Usage**
To pass this check, commit messages should follow the format:
```
type(scope): description
```
Examples:
- `feat(auth): add JWT authentication`
- `fix(ui): resolve button alignment issue`
- `chore(deps): update dependencies`

---

## 2. Nightly Build
### **Triggers**:
- Runs on **every push** to the `main` branch.
- Scheduled to run **daily at 12:00 AM UTC**
- Sends a failure notification via email if test/build/publish fails.

#### **Steps:**
1. Checks out the repository.
2. Copies `.env.example` to `.env`.
3. Installs Docker Compose.
4. Builds and runs containers.
5. Installs and runs tests using `pytest` inside the `CRUD` container.
6. Logs into Registry.
7. Builds and pushes the Docker image.
8. If test/build/publish fails, sends an email notification with build failure details.
9. Retrieves the recipient email.
10. Generates a `send_failure_email.js` script.
 

---

## Contributing
- Follow the [Conventional Commits](https://www.conventionalcommits.org/) standard.
- Submit PRs following best practices.
- Run tests before pushing changes.

---

## License
This project is open-source and available under the MIT License.



## Contributing
I welcome contributions to improve the documentation! You can contribute [here](https://github.com/jod35/fastapi-beyond-crud-docs).
