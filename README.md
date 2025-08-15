# Dare Exchange - Django Project Setup Guide

A Django web application for creating, accepting, and completing dares with user authentication and rating system.

## Prerequisites

Before setting up this project, make sure you have the following installed on your PC:

### 1. Python Installation
- **Download Python 3.8 or higher** from [python.org](https://www.python.org/downloads/)
- During installation, **make sure to check "Add Python to PATH"**
- Verify installation by opening Command Prompt/Terminal and running:
  ```bash
  python --version
  ```

### 2. Git (Optional but Recommended)
- Download from [git-scm.com](https://git-scm.com/downloads)
- This will help you clone and manage the project

## Project Setup Instructions

### Step 1: Get the Project Files

**Option A: If you have the project folder**
- Copy the entire Django project folder to your desired location
- Open Command Prompt/Terminal and navigate to the project folder:
  ```bash
  cd path/to/your/Django/project
  ```

**Option B: If using Git**
- Clone the repository (if available):
  ```bash
  git clone <repository-url>
  cd Django
  ```

### Step 2: Create Virtual Environment

Create a virtual environment to isolate project dependencies:

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate
```

**Note:** You should see `(venv)` at the beginning of your command prompt when activated.

### Step 3: Install Dependencies

Install the required Python packages:

```bash
pip install -r requirements.txt
```

### Step 4: Database Setup

Set up the database and create necessary tables:

```bash
# Apply database migrations
python manage.py migrate

# Create a superuser account (admin)
python manage.py createsuperuser
```

When creating the superuser:
- Enter a username (e.g., admin)
- Enter your email address
- Create a strong password
- Remember these credentials for admin access

### Step 5: Load Sample Data (Optional)

If there are management commands to populate sample data:

```bash
# Check available management commands
python manage.py help

# If populate_dares command exists:
python manage.py populate_dares
```

### Step 6: Run the Development Server

Start the Django development server:

```bash
python manage.py runserver
```

You should see output like:
```
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
December XX, 2024 - XX:XX:XX
Django version 5.2.5, using settings 'dareproject.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
```

### Step 7: Access the Application

Open your web browser and go to:
- **Main Application:** http://127.0.0.1:8000/
- **Admin Panel:** http://127.0.0.1:8000/admin/

## Project Features

- **User Authentication:** Register, login, logout functionality
- **Dare Management:** Create, view, accept, and complete dares
- **Rating System:** Rate completed dares
- **User Profiles:** View user information and dare history
- **Responsive Design:** Works on desktop and mobile devices

## Project Structure

```
Django/
├── dare/                 # Main application
│   ├── models.py        # Database models
│   ├── views.py         # View functions
│   ├── forms.py         # Django forms
│   ├── urls.py          # URL patterns
│   └── management/      # Custom management commands
├── dareproject/         # Project settings
│   ├── settings.py      # Django settings
│   └── urls.py          # Main URL configuration
├── templates/           # HTML templates
├── db.sqlite3          # SQLite database
├── manage.py           # Django management script
└── requirements.txt    # Python dependencies
```

## Troubleshooting

### Common Issues:

1. **"python is not recognized"**
   - Make sure Python is added to your system PATH
   - Try using `py` instead of `python`

2. **"No module named django"**
   - Make sure your virtual environment is activated
   - Run `pip install -r requirements.txt` again

3. **Database errors**
   - Delete `db.sqlite3` file and run `python manage.py migrate` again
   - Make sure you're in the correct project directory

4. **Port already in use**
   - Use a different port: `python manage.py runserver 8001`
   - Or stop any other Django servers running

### Getting Help:

- Check Django documentation: https://docs.djangoproject.com/
- Make sure all commands are run from the project root directory
- Ensure virtual environment is activated before running commands

## Development Notes

- The project uses SQLite database (no additional database setup required)
- Debug mode is enabled (suitable for development only)
- Static files are served automatically in development mode
- The project includes custom management commands for data management

## Next Steps

After successful setup:
1. Create a user account through the web interface
2. Explore the dare creation and acceptance features
3. Test the rating system
4. Access the admin panel to manage users and dares

Enjoy using the Dare Exchange application! 🎯

## Deployment Guide

This project is ready for deployment on various platforms. Choose your preferred deployment method:

### 🚀 Quick Deployment Options

#### Option 1: Railway (Recommended - Free Tier Available)

1. **Fork/Clone the repository** to your GitHub account
2. **Visit [Railway.app](https://railway.app)** and sign up
3. **Create New Project** → **Deploy from GitHub repo**
4. **Select your repository**
5. **Add Environment Variables:**
   ```
   DJANGO_SETTINGS_MODULE=dareproject.production_settings
   SECRET_KEY=your-generated-secret-key
   DEBUG=False
   ALLOWED_HOSTS=your-app-name.railway.app
   ```
6. **Deploy** - Railway will automatically detect Django and deploy!

#### Option 2: Heroku

1. **Install Heroku CLI** and login: `heroku login`
2. **Create Heroku app:**
   ```bash
   heroku create your-app-name
   ```
3. **Set environment variables:**
   ```bash
   heroku config:set DJANGO_SETTINGS_MODULE=dareproject.production_settings
   heroku config:set SECRET_KEY=your-generated-secret-key
   heroku config:set DEBUG=False
   ```
4. **Deploy:**
   ```bash
   git push heroku main
   ```

#### Option 3: PythonAnywhere

1. **Upload your code** to PythonAnywhere
2. **Create a web app** with manual configuration
3. **Set up virtual environment** and install requirements
4. **Configure WSGI file** to point to `dareproject.wsgi`
5. **Set environment variables** in the web app settings

### 🔧 Pre-Deployment Setup

#### Generate Secret Key
```bash
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

#### Collect Static Files (if needed)
```bash
python manage.py collectstatic --noinput
```

#### Create Superuser on Production
```bash
python manage.py createsuperuser
```

### 📋 Environment Variables Required

Copy `.env.example` to `.env` and configure:

- `SECRET_KEY`: Django secret key (generate new one for production)
- `DEBUG`: Set to `False` for production
- `ALLOWED_HOSTS`: Your domain name(s)
- `DATABASE_URL`: Database connection string (auto-provided by most platforms)

### 🗄️ Database Options

**Development:** SQLite (included)
**Production:** PostgreSQL (recommended)

Most deployment platforms provide PostgreSQL databases automatically.

### 📁 Project Structure for Deployment

```
Django/
├── Procfile              # Heroku deployment
├── railway.json          # Railway deployment
├── runtime.txt           # Python version
├── requirements.txt      # Dependencies
├── .env.example         # Environment variables template
├── static/              # Static files directory
├── dareproject/
│   ├── production_settings.py  # Production settings
│   └── settings.py             # Development settings
└── manage.py
```

### 🔒 Security Features

Production settings include:
- SSL redirect
- Secure cookies
- HSTS headers
- XSS protection
- Content type sniffing protection

### 🎯 Post-Deployment Checklist

- [ ] Verify site loads correctly
- [ ] Test user registration/login
- [ ] Create admin superuser
- [ ] Test dare creation and management
- [ ] Verify static files are served
- [ ] Check media file uploads work
- [ ] Test all major functionality

### 🆘 Troubleshooting Deployment

**Static files not loading:**
```bash
python manage.py collectstatic --noinput
```

**Database issues:**
```bash
python manage.py migrate
```

**Environment variables:**
Ensure all required environment variables are set on your deployment platform.

**Logs:**
Check your deployment platform's logs for detailed error messages.

Your Dare Exchange application is now ready for production deployment! 🌟

---

## How to Push This Project to GitHub

1. **Initialize a Git repository (if not already initialized):**
   ```bash
   git init
   ```

2. **Add all project files:**
   ```bash
   git add .
   ```

3. **Commit your changes:**
   ```bash
   git commit -m "Initial commit of Dare Exchange Django project"
   ```

4. **Create a new repository on [GitHub](https://github.com/new)**  
   - Name it (e.g., `dare-exchange`)
   - Do **not** initialize with README/other files (since you already have them)

5. **Add the remote repository:**
   ```bash
   git remote add origin https://github.com/<your-username>/<your-repo-name>.git
   ```

6. **Push your project to GitHub:**
   ```bash
   git push -u origin master
   ```
   *(If using `main` branch, replace `master` with `main`)*

7. **Done!**  
   Your project is now on GitHub.  
   You can view it at: `https://github.com/<your-username>/<your-repo-name>`