docker-trac-standalone
======================

Docker images for running a standalone Trac instance (git, or with svnserve included).

## Images

* Trac 0.12: a Docker image to run Trac 0.12 in a container together with svnserve (via supervisord). *Deprecated.* Mostly untested.
* Trac 1.0-svn: a Docker image to run Trac 1.0 in a container together with svnserve (via supervisord).
* Trac 1.0-git: a Docker image to run Trac 1.0 in a container, using a (local) git repository.

## Expected volumes

* `/trac`: the Trac environment, with the configuration file in `conf/trac.ini`, sqlite database in `db/trac.sqlite`, etc.
* `/svn`: the SVN repository
* `/git`: the local git repository

## Execution

### Trac 1.0-svn:

    docker run -ti --rm --volume /data/myproj/tracenv:/trac --volume /data/myproj/svn:/svn --volume /data/myproj/supervisor_logs:/var/log/supervisor -p 80:80 -p 3690:3690 trac
 
### Trac 1.0-git:
    
    docker run -ti --rm --volume /data/myproj/tracenv:/trac --volume /data/myproj/git:/git -p 80:80 trac

## `trac.ini` excerpt/example for Trac 1.0-git

    [components]
    tracopt.versioncontrol.git.* = enabled

    [account-manager]
    password_store = SessionStore
    hash_method = HtDigestHashMethod

    [trac]
    base_url = http://example.com/
    database = sqlite:/trac/db/trac.sqlite
    repository_type = git
    repository_dir = /git
