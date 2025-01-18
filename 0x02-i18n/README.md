# ALX Backend i18n Project

## Overview
This project implements internationalization (i18n) in a Flask web application. It demonstrates how to handle multiple languages, locales, and timezones using Flask-Babel.

## Requirements
- Ubuntu 18.04 LTS
- Python 3.7
- Flask
- Flask-Babel 2.0.0
- pytz

## Installation
```bash
# Install required packages
pip3 install flask flask_babel==2.0.0 pytz
```

## Project Structure
```
0x02-i18n/
│
├── 0-app.py               # Basic Flask app
├── 1-app.py               # Basic Babel setup
├── 2-app.py               # Get locale from request
├── 3-app.py               # Parametrize templates
├── 4-app.py               # Force locale with URL parameter
├── 5-app.py               # Mock login system
├── 6-app.py               # User locale preferences
├── 7-app.py               # Timezone handling
├── app.py                 # Final application with time display
├── babel.cfg              # Babel configuration
│
├── templates/
│   ├── 0-index.html
│   ├── 1-index.html
│   ├── 2-index.html
│   ├── 3-index.html
│   ├── 4-index.html
│   ├── 5-index.html
│   ├── 6-index.html
│   ├── 7-index.html
│   └── index.html
│
└── translations/
    ├── en/
    │   └── LC_MESSAGES/
    │       ├── messages.mo
    │       └── messages.po
    └── fr/
        └── LC_MESSAGES/
            ├── messages.mo
            └── messages.po
```

## Features
- Multiple language support (English and French)
- Locale detection from URL parameters
- User timezone preferences
- Mock user login system
- Template parameterization
- Current time display based on locale

## Usage
1. Start the Flask application:
```bash
python3 app.py
```

2. Access the application:
- Default: `http://127.0.0.1:5000/`
- With locale: `http://127.0.0.1:5000/?locale=[fr|en]`
- With login: `http://127.0.0.1:5000/?login_as=[user_id]`

## Translation Management
```bash
# Extract messages
pybabel extract -F babel.cfg -o messages.pot .

# Initialize translations
pybabel init -i messages.pot -d translations -l en
pybabel init -i messages.pot -d translations -l fr

# Compile translations
pybabel compile -d translations
```

## Testing
The application includes test cases for:
- Basic routing
- Language switching
- Timezone handling
- User preferences
- Template rendering

## Author
Martin Nyemba

ALX Backend Development Program

## License
Copyright © 2025 ALX, All rights reserved.
