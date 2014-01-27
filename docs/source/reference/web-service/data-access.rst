Data Access
###########

This set of APIs is for accessing data defined by content authors or collect
during the session.

.. contents::

GET /storage/ticket/
====================

Retrieve a list of tickets.

Paramaters via Query String
---------------------------

======= ======== ======== ======= ========================================================
Key     Type     Required Default Description
======= ======== ======== ======= ========================================================
page    int, >0  No       1       The page number
size    int, >0  No       8       The number of results per page
role    str      No       \-      The role of the ticket owner
user    int/hash No       \-      The user identifier
session int/hash No       \-      The session identifier
======= ======== ======== ======= ========================================================

Response
--------

.. code-block:: javascript

    {
        "query": STR_GIVEN_QUERY_OR_NULL,
        "page": INT_PAGE_NUMBER,
        "size": NUMBER_OF_RESULT_PER_PAGE,
        "list": [
            // List of response object defined in GET /storage/ticket/ID
        ]
    }

GET /storage/ticket/ID[?enable=url]
===================================

Retrieve a ticket by identifier.

``?enable=url`` is to include ``_url``, a full
URL (with default options) to the entity. The option is omitted by default.

Response by default
-------------------

Suppose we send a **GET** request (TLS) to ``https://api.eryri.org/storage/ticket/ca23bcdf8fade``
where **api.eryri.org** is the host name.

.. code-block:: javascript

    {
        "id": "ca23bcdf8fade",
        "session": "218bycp89eyfse",
        "user": "f923runcp9usdf",
        "role": "attendee",
        "status": "used",
        "created": 1390788719.938647,
        "updated": 1390788719.938647
    }

Response with enable=url
------------------------

Suppose we send a **GET** request (TLS) to ``https://api.eryri.org/storage/ticket/ca23bcdf8fade?enable=url``
where **api.eryri.org** is the host name.

.. code-block:: javascript

    {
        "_url": https://api.eryri.org/storage/ticket/ca23bcdf8fade,
        "id": "ca23bcdf8fade",
        "session": {
            "_url": "https://api.eryri.org/storage/session/218bycp89eyfse",
            "id": "218bycp89eyfse"
        },
        "user": {
            "_url": "https://api.eryri.org/security/user/f923runcp9usdf",
            "id": "f923runcp9usdf"
        },
        "role": "attendee",
        "status": "used",
        "created": 1390788719.938647,
        "updated": 1390788719.938647
    }

POST /storage/ticket
====================

Create a ticket.

Suppose we want to create the sample ticket mentioned in **GET /storage/ticket/ID[?enable=url]**
where session ID is ``218bycp89eyfse`` and user ID is ``f923runcp9usdf``.

Request
-------

.. code-block:: javascript

    {
        "session": "218bycp89eyfse",
        "user": "f923runcp9usdf",
        "role": "attendee"
    }

where the **created** and **updated** properties are auto-generated and **status**
is always reset to **valid**.

Response
--------

.. code-block:: javascript

    {
        "id": "ca23bcdf8fade",
        "session": "218bycp89eyfse",
        "user": "f923runcp9usdf",
        "role": "attendee",
        "status": "valid",
        "created": 1390788719.938647,
        "updated": 1390788719.938647
    }

PUT /storage/ticket/ID
======================

Update a ticket by ID.

Suppose we want to update the sample ticket mentioned in **GET /storage/ticket/ID[?enable=url]**
where status is **used**.

Request
-------

.. code-block:: javascript

    {
        "status": "used",
        "role": "observer"
    }

Response
--------

A successful response is **HTTP-200**.

.. code-block:: javascript

    {
        "id": "ca23bcdf8fade",
        "session": "218bycp89eyfse",
        "user": "f923runcp9usdf",
        "role": "observer",
        "status": "used",
        "created": 1390788719.938647,
        "updated": 1390788719.938647
    }

DELETE /storage/ticket/ID
=========================

Delete a ticket by ID.

Response
--------

Use a simple response scheme defined in "How it normally works" in
:doc:`/architecture/web-service`.