# get base image
FROM python:3.12

# Set working directory
WORKDIR /app

# copy requirements first to leverage Docker cache
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt
RUN pip install gunicorn


# Copy project
COPY . .

# create static and media directories
RUN mkdir -p /app/staticfiles /app/media

# collect static files
RUN python manage.py collectstatic --noinput

# Expose port
EXPOSE 8000

# Command to run when container starts
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "fitness_booking.wsgi:application"]