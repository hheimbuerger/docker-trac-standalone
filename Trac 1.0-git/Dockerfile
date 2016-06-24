FROM python:2.7

# Install sqlite3 command line utilities - we don't actually need those, but it's convenient for troubleshooting
RUN apt-get update && \
    apt-get install -y git sqlite3 libsqlite3-dev && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

COPY requirements.txt /tmp
RUN pip install --no-cache-dir -r /tmp/requirements.txt

VOLUME ["/trac", "/git"]

EXPOSE 80

CMD ["/usr/local/bin/tracd", "--single-env", "/trac"]
