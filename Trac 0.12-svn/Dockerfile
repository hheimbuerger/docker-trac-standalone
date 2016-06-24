FROM python:2.7-slim

# Install supervisor, svnserve and the Python-SVN bindings needed by Trac
RUN apt-get update && \
    apt-get install -y supervisor subversion python-subversion && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/*

# This is just needed because the python-subversion installs its Python modules (e.g. svn.core) into dist-packages, which by default isn't in the PYTHONPATH (see https://serverfault.com/questions/388420/python-svn-bindings-importerror-no-module-named-svn)
COPY dist-packages.pth /usr/local/lib/python2.7/site-packages/dist-packages.pth

# Install Trac and plugins from the requirements file
COPY requirements.txt /tmp
RUN pip install --no-cache-dir -r /tmp/requirements.txt

# Define our volumes: /trac should be mounted to the 'Trac environment' and /svn to the SVN repository
VOLUME ["/trac", "/svn"]

# Export ports 80 (HTTP, by tracd) and 3690 (SVN, by svnserve)
EXPOSE [80, 3690]

# Run supervisor, as configured in supervisord.conf, running svnserve and tracd in parallel
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
CMD ["/usr/bin/supervisord"]
