# Define function directory
ARG FUNCTION_DIR="/src"

FROM mcr.microsoft.com/playwright/python:v1.49.0-jammy as build-image

# Install aws-lambda-cpp build dependencies
RUN apt-get update && \
    apt-get install -y \
    g++ \
    make \
    cmake \
    unzip \
    libcurl4-openssl-dev 
# Include global arg in this stage of the build
ARG FUNCTION_DIR
# Create function directory
RUN mkdir -p ${FUNCTION_DIR}

# Copy function code
COPY ./src ${FUNCTION_DIR}

# Install Playwright
RUN pip3 install playwright

# Run Playwright install to ensure all necessary browser binaries are installed
RUN playwright install

# Multi-stage build: grab a fresh copy of the base image
FROM mcr.microsoft.com/playwright/python:v1.49.0-jammy
# Include global arg in this stage of the build
ARG FUNCTION_DIR
# Set working directory to function root directory
WORKDIR ${FUNCTION_DIR}

# Copy in the build image dependencies
COPY --from=build-image ${FUNCTION_DIR} ${FUNCTION_DIR}
# Install the dependencies
RUN pip install --no-cache-dir -r requirements.txt

CMD [ "uvicorn","main:app", "--host","0.0.0.0", "--port", "80" ]
