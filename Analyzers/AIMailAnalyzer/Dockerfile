#########
# FINAL #
#########

# pull official base image
FROM python:3.10-slim

ENV http_proxy="http://10.10.10.10:8080"
ENV https_proxy="http://10.10.10.10:8080"

RUN apt-get update -y && \
    apt-get upgrade -y && \
    rm -rf /var/lib/apt/lists/*

COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# set work directory
WORKDIR /worker/

# install dependencies
COPY requirements.txt .
RUN uv pip install --system --upgrade pip
RUN uv pip install --system --no-cache torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
RUN uv pip install --system --no-cache -r requirements.txt

COPY . /worker/AIMailAnalyzer/

# Expose the application
ENTRYPOINT ["python","AIMailAnalyzer/ai_mail_classifier.py"]
