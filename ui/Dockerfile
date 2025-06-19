# Dockerfile for Streamlit UI
FROM python:3.9-slim

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY streamlit_app.py .

# Create necessary directories
RUN mkdir -p /app/.streamlit

# Configure Streamlit
RUN echo '[server]\n\
headless = true\n\
port = 8501\n\
address = "0.0.0.0"\n\
enableCORS = false\n\
enableXsrfProtection = false\n\
' > /app/.streamlit/config.toml

# Set environment variables
ENV PYTHONPATH=/app
ENV API_BASE_URL=https://oopsallaiapi.azurewebsites.net

# Expose port
EXPOSE 8501


# Run the application
CMD ["streamlit", "run", "streamlit_app.py", "--server.address", "0.0.0.0", "--server.port", "8501"]
