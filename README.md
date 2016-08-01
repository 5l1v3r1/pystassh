[![Build Status](https://travis-ci.org/julienc91/pystassh.png)](https://travis-ci.org/julienc91/pystassh)
[![Coverage Status](https://coveralls.io/repos/github/julienc91/pystassh/badge.svg?branch=master)](https://coveralls.io/github/julienc91/pystassh?branch=master)
[![Documentation](https://readthedocs.org/projects/pystassh/badge/?version=latest)](http://pystassh.readthedocs.org/en/latest/)

pystassh
========

An easy to use libssh wrapper to execute commands on a remote server via SSH with Python.

* Author: Julien CHAUMONT (https://julienc.io)
* Version: 1.0
* Date: 2016-07-30
* Licence: MIT
* Url: http://github.com/julienc91/pystassh

Installation
------------

Just use `pip` to install the package:

    pip install pystassh
    
`pystassh` is working with python 2.7, python 3+ and pypy.

Requirements
------------

`pystassh` is using libssh to work, you will have to install the library before using
`pystassh`. Only version 0.7.3 was used during the development, but versions 0.5 and above should work fine as well with `pystassh`.
Visit [libssh's official website](https://www.libssh.org/get-it/) for more information.

On Debian and Ubuntu:

    apt-get install libssh-4
    
On Fedora:

    dnf install libssh

Examples
--------

Running simple commands:

    >>> from pystassh import Session
    >>> with Session('remote_host.org', username='foo', password='baz') as ssh_session:
    ...     res = ssh_session.execute('whoami')
    >>> res.stdout
    'foo'
    
Handling errors:

    >>> from pystassh import Session
    >>> with Session('remote_host.org', username='foo', password='baz') as ssh_session:
    ...     res = ssh_session.execute('whoam')
    >>> res.stderr
    'bash: whoam : command not found'
    
Running multiple commands:

    >>> from pystassh import Session
    >>> with Session('remote_host.org', username='foo', password='baz') as ssh_session:
    ...     ssh_session.execute('echo "bar" > /tmp/foo')
    ...     res = ssh_session.execute('cat /tmp/foo')
    >>> res.stdout
    'bar'
    
Use a session without a `with` block:

    >>> from pystassh import Session
    >>> ssh_session = Session('remote_host.org', username='foo', password='baz')
    >>> ssh_session.connect()
    >>> res = ssh_session.execute('whoami')
    >>> res.stdout
    'foo'
    >>> ssh_session.disconnect()


Documentation
-------------

The complete documentation is available at: http://pystassh.readthedocs.org/en/latest/