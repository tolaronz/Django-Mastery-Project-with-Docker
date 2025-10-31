**Table of Contents:**

- [About The Project](#about-the-project)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
    - [Python installation on Ubuntu](#python-installation-on-ubuntu)
    - [PostgreSQL installation on Ubuntu](#postgresql-installation-on-ubuntu)
- [Installation](#installation)
  - [Virtual Environment (`venv`)](#virtual-environment-venv)
  - [Environment Configuration](#environment-configuration)
  - [Database Setup](#database-setup)
  - [Running the project](#running-the-project)
- [Heroku Deployment](#heroku-deployment)
  - [Quick Deploy](#quick-deploy)
- [Documentation](#documentation)
  - [Quick Start](#quick-start)
  - [Deployment](#deployment)
  - [Upgrade \& Migration](#upgrade--migration)
  - [Security](#security)
  - [Scripts](#scripts)
- [Roadmap](#roadmap)
- [Contributing](#contributing)

<!-- ABOUT THE PROJECT -->
## About The Project

A modern Django 5.1 portfolio/showcase website built with:

- **Backend**: Django 5.1.3 (LTS) with Python 3.13
- **Database**: PostgreSQL with psycopg3
- **Frontend**: Bootstrap 4 and vanilla JavaScript  
- **Deployment**: Ready for Heroku, DigitalOcean, or AWS
- **Features**: 
  - Environment-based configuration
  - Production-ready security settings
  - Static file handling with WhiteNoise
  - Comprehensive documentation

**Perfect for**: Portfolio sites, showcases, or as a starting template for Django projects.

<!-- GETTING STARTED -->
## Getting Started

For development, you will need **Python 3.12 or higher**, pip, venv, and PostgreSQL installed in your environment.

> **For Forkers**: This project is ready to fork and deploy! See [docs/quick-start.md](docs/quick-start.md) to get started.
> 
> **Upgrading**: If you're upgrading an older Django 3.0 project, see [docs/upgrade-guide.md](docs/upgrade-guide.md).

### Prerequisites

* A good understanding of web development (HTML, CSS, JavaScript)
* Basic knowledge of Python and SQL database systems
* Familar with Django framework for front-end and back-end development
* Object-oriented Programming (OOP) paradigm
* Model-View-Controller (MVC) paradigm
* Model-View-ViewMode (MVVM) paradigm
* Knowledge and use of the Command-line Interface (CLI)

#### Python installation on Ubuntu

On Ubuntu 20.04 and later, Python 3 comes pre-installed. Check first to see if you have the tools required already installed:

    $ python3 --version
    $ pip3 --version

Head over to the [official Python website](https://www.python.org/downloads/) and download the installer
Also, be sure to have `git` donwloaded and available in your PATH as well.

You can install Python and pip easily with apt install, just run the following commands:

    $ sudo apt install python3
    $ sudo apt install python3-pip

There are a few more packages and development tools to install to ensure that we have a robust setup for our programming environment:

    $ sudo apt install -y build-essential libssl-dev libffi-dev python3-dev

If you need to update `pip`, you can make it using `pip`! Cool right? After running the following command, just open again the command line and be happy.

    $ python3 -m pip install --upgrade pip

#### PostgreSQL installation on Ubuntu

Installation of PostgreSQL via CLI:

```bash
# Create the file repository configuration:
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# Import the repository signing key:
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Update the package lists:
sudo apt-get update

# Install the latest version of PostgreSQL.
# If you want a specific version, use 'postgresql-12' or similar instead of 'postgresql':
sudo apt-get install postgresql
```

Installation of the pgAdmin GUI:

```bash
$ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc |
sudo apt-key add -
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/
`lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
$ sudo apt-get update
$ sudo apt-get install pgadmin4 pgadmin4-apache2 -y
```

Please note for sake of ease, this project is set to work with the default configurations of PostgreSQL on a local installation.


## Installation

    $ git clone https://github.com/brennanbrown/django-project.git
    $ cd django-project

### Virtual Environment (`venv`)

While there are a few ways to achieve a programming environment in Python, we’ll be using the venv module here, which is part of the standard Python 3 library. Let’s install venv by typing:

    $ sudo apt install python3.12-venv

Creating and entering a new virtual environment:

    $ python3.12 -m venv env
    $ source env/bin/activate  # On Windows: env\Scripts\activate
    $ pip install --upgrade pip
    $ pip install -r requirements.txt

You can ensure that you're in your new virtual environment if you see `(env)` prepend your bash shell:

    (env) user@ubuntu:~/django_project$ 

### Environment Configuration

Copy the example environment file and configure it:

    $ cp .env.example .env
    $ nano .env  # or use your preferred editor

Generate a secure SECRET_KEY:

    $ python -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())'

Add the generated key and your database settings to `.env`:

```
SECRET_KEY=your-generated-secret-key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
DB_NAME=portfoliodb
DB_USER=postgres
DB_PASSWORD=your-postgres-password
```

### Database Setup

Create the database and run migrations:

    $ sudo -u postgres psql -c "CREATE DATABASE portfoliodb;"
    $ python manage.py migrate
    $ python manage.py createsuperuser

### Running the project

    $ python manage.py runserver

Once the server has started up, you can visit it at [localhost:8000/](localhost:8000/), or [127.0.0.1:8000/](127.0.0.1:8000/).

## Heroku Deployment

Deploy to Heroku in 5 minutes! See [docs/heroku-quickstart.md](docs/heroku-quickstart.md) for quick deployment or [docs/heroku-deployment.md](docs/heroku-deployment.md) for complete documentation.

### Quick Deploy

**Option 1: Automated Script**
```bash
./scripts/deploy-to-heroku.sh
```

**Option 2: Manual Commands**
```bash
heroku create your-app-name
heroku addons:create heroku-postgresql:essential-0
heroku config:set SECRET_KEY="$(python -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())')"
heroku config:set DEBUG="False"
heroku config:set ALLOWED_HOSTS="your-app-name.herokuapp.com"
git push heroku main
heroku run python manage.py createsuperuser
heroku open
```

**Option 3: GitHub Integration (No CLI needed)**

See [docs/heroku-github-deploy.md](docs/heroku-github-deploy.md) for step-by-step instructions to deploy directly from GitHub via Heroku's web interface.

## Documentation

Complete documentation is available in the [docs/](docs/) directory:

### Quick Start
- **[Quick Start Guide](docs/quick-start.md)** - Get running in minutes
- **[Heroku Quick Start](docs/heroku-quickstart.md)** - Deploy to Heroku fast

### Deployment
- **[Heroku Deployment](docs/heroku-deployment.md)** - Complete deployment guide
- **[Heroku GitHub Integration](docs/heroku-github-deploy.md)** - Deploy via GitHub
- **[Deployment Checklist](docs/heroku-checklist.md)** - Step-by-step checklist

### Upgrade & Migration
- **[Upgrade Guide](docs/upgrade-guide.md)** - Django 3.0 → 5.1 migration
- **[Changes Summary](docs/changes-summary.md)** - Overview of changes
- **[Upgrade Checklist](docs/upgrade-checklist.md)** - Migration checklist

### Security
- **[Security Policy](docs/security.md)** - Best practices & vulnerability reporting

### Scripts
- **[Deploy to Heroku](scripts/deploy-to-heroku.sh)** - Automated deployment script

See the [docs/README.md](docs/README.md) for a complete documentation index.

<!-- ROADMAP -->
## Roadmap

See the [open issues](https://github.com/brennanbrown/django-project/issues) for a list of proposed features (and known issues).

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request
