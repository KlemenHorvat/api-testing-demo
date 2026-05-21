FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY locustfile.py .

# Default: run headless for 30 seconds, 10 users, spawn rate 2
# TWEAKED: removed error override (reintroduced exist code 1 on error) to allow CI to fail on test failures. Adjusted RPS to account for hard limit on target.
CMD ["locust", "--headless", "--run-time", "30s", "--users", "6", "--spawn-rate", "2", "--exit-code-on-error", "1", "--host", "https://hapi.fhir.org", "-f", "locustfile.py"]
