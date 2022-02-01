FROM python:alpine
FROM python:3.7.5
RUN python3 -m pip install -U pip
RUN python3 -m pip install -U setuptools
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
RUN pip install flask

FROM ubuntu:20.04
RUN groupadd flaskgroup 
RUN useradd -m -g flaskgroup -s /bin/bash flask
RUN echo "flask ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
RUN mkdir -p /home/flask/app/web
WORKDIR /home/flask/app/web
RUN chown -R flask:flaskgroup /home/flask
USER flask
ENTRYPOINT ["/usr/local/bin/gunicorn", "--bind", ":8000", "linode:app", "--reload", "--workers", "16"]
