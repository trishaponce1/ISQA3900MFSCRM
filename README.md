# Maverick Food Services CRM

A multi-table **Django** web application built as a Customer Relationship Management (CRM) system for a fictitious campus food services organization. Developed as part of ISQA 3900 at the University of Nebraska Omaha and deployed to PythonAnywhere.

## About the Project

Maverick Food Services (MFS) is a campus catering provider that needs to track its customers, the services it provides (event catering, setup/cleanup), and the products it sells. This CRM allows food service managers to manage customer records, log service and product transactions, and generate per-customer summary reports — all through a role-based web interface with authentication.

### Key Features

- **Customer Management** — Full CRUD operations for customer records including name, organization, account number, address, and contact details.
- **Service Tracking** — Log catering services provided to customers with category, location, setup/cleanup times, and charges.
- **Product Tracking** — Record products sold to customers with descriptions, quantities, pickup times, and charges.
- **Customer Summary Report** — Aggregated view of all services and products for a given customer, with calculated totals using Django's `Sum` aggregation and `django-mathfilters`.
- **Role-Based Access** — Admin users manage everything via the Django admin panel; employees access customer, service, and product data through the front-end interface.
- **Authentication** — Login/logout with `@login_required` protection on all data views. Password reset functionality with email integration.

## Tech Stack

| Layer | Technology |
|-------|------------|
| Backend | Python 3.8, Django 3.x |
| Database | SQLite (development) |
| Frontend | Django Templates, Bootstrap 3, HTML/CSS |
| Libraries | django-mathfilters, django.contrib.humanize |
| Deployment | PythonAnywhere |
| IDE | PyCharm |

## Data Models

The application uses three interconnected models:

- **Customer** — Name, organization, role, email, building/room, address, account number, city, state, zip, phone, and timestamps.
- **Service** — Linked to a Customer via ForeignKey. Tracks service category, description, location, setup time, cleanup time, and service charge.
- **Product** — Linked to a Customer via ForeignKey. Tracks product name, description, quantity, pickup time, and charge.

Deleting a customer cascades to remove all associated service and product records.

## Project Structure

```
ISQA3900MFSCRM/
├── MaverickFoodServices/         # Django project settings
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── crm/                          # Main application
│   ├── migrations/
│   ├── templates/crm/            # HTML templates
│   │   ├── base.html             # Navigation & layout
│   │   ├── home.html             # Landing page
│   │   ├── customer_list.html    # Customer table with CRUD actions
│   │   ├── customer_edit.html    # Customer add/edit form
│   │   ├── service_list.html     # Service table with CRUD actions
│   │   ├── service_new.html      # Add service form
│   │   ├── service_edit.html     # Edit service form
│   │   ├── product_list.html     # Product table with CRUD actions
│   │   ├── summary.html          # Per-customer summary report
│   │   └── ...
│   ├── admin.py                  # Admin panel configuration
│   ├── forms.py                  # ModelForms for Customer, Service, Product
│   ├── models.py                 # Data models
│   ├── urls.py                   # App URL routing
│   └── views.py                  # View functions (all @login_required)
├── templates/registration/       # Auth templates (login)
├── manage.py
└── requirements.txt
```

## What I Learned

This project was a significant step up from the single-model LocalLibrary tutorial. Building the MFS CRM taught me how to work with **multi-table relational data** in Django — defining ForeignKey relationships, cascading deletes, and querying across related models. I implemented the full **CRUD pattern** (create, read, update, delete) for three separate entities, built **Django ModelForms** for user-facing data entry, and used **Django's aggregation framework** (`Sum`) alongside `django-mathfilters` and `django.contrib.humanize` to produce formatted summary reports. I also gained practical experience with **role-based access control**, **deployment to PythonAnywhere**, and **Git-based code management** as part of the development workflow.

## How to Run

```bash
# Clone the repository
git clone https://github.com/trishaponce1/ISQA3900MFSCRM.git
cd ISQA3900MFSCRM

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Apply migrations and create a superuser
python manage.py migrate
python manage.py createsuperuser

# Start the development server
python manage.py runserver
```

Visit `http://127.0.0.1:8000/` for the home page or `http://127.0.0.1:8000/admin/` for the admin panel.

