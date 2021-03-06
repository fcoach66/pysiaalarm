==========
pysiaalarm
==========


Python package for creating a client that talks with SIA-based alarm systems.  Currently tested using a Ajax Systems alarm system. If you have other systems please reach out.


Description
===========

This package was created to talk with alarm systems using the SIA protocal, it was tested using a Ajax system, but should support all defined SIA codes. 
It creates a new thread with a TCP Server or a asyncio coroutine running bound to a host and port, the alarm system acts a client that sends messages to that server and the server acknowledges the messages and call the supplied function.


Config 
==========

For threaded:

.. code-block:: python

    from pysiaalarm import SIAClient, SIAAccount

For asyncio:

.. code-block:: python

    from pysiaalarm.aio import SIAClient, SIAAccount


The SIAClient takes these arguments:

- host: if there is a specific host to talk to, usually has '' for localhost.
- port: the TCP port your alarm system communicates with.
- accounts: list of type SIAAccount that are to be allowed to send messages to this server
- function: a function that will be called for every event that it handles, takes only a SIAEvent as parameter and does not pass back anything.

SIAAccount takes these arguments:

- account_id: the account id as 3-16 ASCII hex characters.
- [optional] key: encryption key specified in your alarm system 16, 24, or 32 ASCII characters
- [optional] allowed_timeband: encrypted messages have a timestamp and those are checked against this timeband, by default the timestamp is allowed between -40 and +20 seconds comparing the timestamp in the message and the current timestamp of the system running the server.
