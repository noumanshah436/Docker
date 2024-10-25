# Use Python 3.12 as the base image
FROM python:3.12

# Set the working directory in the container
WORKDIR /code

# Copy the requirements.txt file into the container code dir
COPY ./requirements.txt /code/requirements.txt

# Install dependencies
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

# Copy the FastAPI app code into the container
COPY ./app /code/app

# Correctly use Uvicorn to run the FastAPI app
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]

# FastAPI in Containers - Docker ( for more detail about this file)
# https://fastapi.tiangolo.com/deployment/docker/#create-the-fastapi-code