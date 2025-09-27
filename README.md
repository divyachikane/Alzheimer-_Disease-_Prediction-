# Alzheimer's MRI Classification Django App

A Django web application for Alzheimer's disease detection using deep learning models. This application provides a user-friendly interface for uploading MRI scans and getting AI-powered predictions for different stages of dementia.

## Features

- **User Authentication**: Secure login system with Django's built-in authentication
- **MRI Image Upload**: Upload and preview MRI scans for analysis
- **AI Prediction**: Real-time classification using Keras/TensorFlow models
- **Model Management**: Admin-only interface for uploading and managing ML models
- **Performance Visualization**: Charts and metrics showing model accuracy
- **Responsive Design**: Mobile-friendly interface with Bootstrap 5

## Requirements

- Python 3.8+
- Django 4.2.0
- TensorFlow 2.10.0
- Pillow (PIL)
- NumPy

## Installation

1. **Clone or download the project files**

2. **Create a virtual environment**:
   ```bash
   python -m venv alzheimer_env
   source alzheimer_env/bin/activate  # On Windows: alzheimer_env\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up the database**:
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

5. **Create a superuser account**:
   ```bash
   python manage.py createsuperuser
   ```
   Follow the prompts to create an admin account.

6. **Create required directories**:
   ```bash
   mkdir -p predictor/ml_models
   mkdir -p predictor/static/predictor/images
   mkdir -p predictor/static/predictor/data
   mkdir -p media/uploads
   ```

7. **Add your model file**:
   Place your Keras model file at: `predictor/ml_models/Alzheimer_MRI_4_classes_model.h5`

8. **Add accuracy charts (optional)**:
   - Place accuracy chart: `predictor/static/predictor/images/Alzheimer_MRI_4_classes_accuracy.png`
   - Place loss chart: `predictor/static/predictor/images/Alzheimer_MRI_4_classes_loss.png`
   - Place training data: `predictor/static/predictor/data/training_history.csv`

## Running the Application

1. **Start the development server**:
   ```bash
   python manage.py runserver
   ```

2. **Access the application**:
   - Main app: http://127.0.0.1:8000/
   - Admin panel: http://127.0.0.1:8000/admin/

## Usage Guide

### For Regular Users

1. **Login**: Use the login page to authenticate
2. **Upload MRI**: Navigate to the home page and upload an MRI scan
3. **View Results**: Get prediction results with confidence scores and descriptions
4. **View Accuracy**: Check the accuracy page for model performance metrics

### For Administrators

1. **Login as superuser**: Use your admin credentials
2. **Upload Models**: Access the "Upload Model" option in the user dropdown
3. **Manage Models**: View and manage different model versions
4. **Admin Panel**: Access Django admin for user and data management

## Model Requirements

The application expects:
- **Input Shape**: (128, 128, 3) - RGB images resized to 128x128 pixels
- **Output Classes**: 4 classes in this order:
  1. Non-Demented
  2. Very Mild Demented
  3. Mild Demented
  4. Moderate Demented
- **File Format**: Keras .h5 format
- **File Size**: Maximum 100MB

## File Structure

```
alzheimer_project/
├── alzheimer_project/          # Django project settings
├── predictor/                  # Main Django app
│   ├── templates/             # HTML templates
│   ├── static/               # CSS, JS, images
│   ├── ml_models/            # ML model files (.h5)
│   ├── migrations/           # Database migrations
│   ├── views.py             # View functions
│   ├── models.py            # Database models
│   ├── forms.py             # Django forms
│   ├── urls.py              # URL routing
│   └── ml_utils.py          # ML utility functions
├── media/                    # User uploaded files
├── manage.py                # Django management script
└── requirements.txt         # Python dependencies
```

## Test Plan

### 1. Authentication Testing
```bash
# Create test superuser
python manage.py createsuperuser
# Username: savi
# Password: 12345678
```
### 3. Prediction Testing
1. Login as any user
2. Upload an MRI image (JPG/PNG format)
3. Click "Analyze Scan"
4. Verify prediction results display correctly

### 4. Accuracy Page Testing
1. Navigate to Accuracy page
2. Verify static charts load (if images are present)
3. Check performance metrics table

## Production Deployment

For production deployment:

1. **Set DEBUG = False** in settings.py
2. **Configure allowed hosts** in settings.py
3. **Use a production database** (PostgreSQL recommended)
4. **Serve static/media files** with nginx or Apache
5. **Use WSGI server** like Gunicorn:
   ```bash
   gunicorn alzheimer_project.wsgi:application
   ```

## Security Notes

- Model upload is restricted to superusers only
- File upload validation prevents arbitrary file execution
- CSRF protection enabled for all forms
- User authentication required for predictions

## Troubleshooting

### Common Issues

1. **Model not loading**: Ensure the .h5 file is in the correct location
2. **TensorFlow errors**: Verify TensorFlow 2.10.0 is installed
3. **Image upload fails**: Check file permissions on media directory
4. **Static files not loading**: Run `python manage.py collectstatic`

### Error Messages

- "Model not available": Check model file path and permissions
- "Invalid image format": Ensure uploaded file is a valid image
- "Permission denied": Verify user has appropriate access rights

## Support

For issues or questions:
1. Check the Django logs for detailed error messages
2. Verify all dependencies are correctly installed
3. Ensure model file format matches requirements
4. Check file permissions for media and static directories

## License

This project is for educational and research purposes. Please ensure compliance with medical data regulations when using in production environments.