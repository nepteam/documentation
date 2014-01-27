Security
########

.. contents::

POST /security/authentication
=============================

Perform the user authentication

Request
-------

Format
~~~~~~

.. code-block:: javascript

    {
        "key": E_MAIL_AS_KEY,
        "password": PASSWORD
    }

Example
~~~~~~~

.. code-block:: javascript

    {
        "key": "ramen@food.org",
        "password": "magic-word"
    }

Response
--------

This API returns an **empty HTTP-200** response if succeeded.

This API returns an **empty HTTP-400** response if the parameter ``key`` (as
e-mail address) is invalid or any fields are empty or empty string.

This API returns an **empty HTTP-401** response if the authentication fails.

This API returns an **empty HTTP-403** response if the token is invalid.

GET /security/users
===================

Retrieve the list of users or run the case-insensitive search for users by alias,
full name or e-mail address.

Parameters via Query String
---------------------------

===== ======= ======== ======= ========================================================
Key   Type    Required Default Description
===== ======= ======== ======= ========================================================
page  int, >0 No       1       The page number
size  int, >0 No       8       The number of results per page
query str     No       \-      The search query for alias, full name or e-mail address.
===== ======= ======== ======= ========================================================

Response
--------

The result will always be in a JSON-formatted HTTP-200 response like the following.

.. code-block:: javascript

    {
        "query": STR_GIVEN_QUERY_OR_NULL,
        "page": INT_PAGE_NUMBER,
        "size": NUMBER_OF_RESULT_PER_PAGE,
        "list": [
            // List of response object defined in GET /security/users/ID_OR_EMAIL_ADDRESS
        ]
    }

.. note:: The search result will order by e-mail address, alias and full name.

GET /security/users/ID_OR_EMAIL_ADDRESS
=======================================

Retrieve the user information (without security-sensitive information) by an
identifier or an e-mail address.

The parameter ``ID_OR_EMAIL_ADDRESS`` can be either an e-mail address (by pattern)
or a user (unique) identifier.

Response
--------

The result will always be in a JSON-formatted HTTP-200 response like the following.

.. code-block:: javascript

    {
        "_method": "identifier", // "email"
        // non-security-sensitive user properties
        "id": USER_IDENTIFIER,
        "name": USER_NAME,
        // ...
    }

PUT /security/users/ID_OR_EMAIL_ADDRESS
=======================================

Update the user by an identifier or an e-mail address.

Request
-------

The content body should indicate which properties to update in JSON. For example,
suppose we want to update the name of the user.

.. code-block:: javascript

    {
        "name": "ジュティ"
    }

DELETE /security/users/ID_OR_EMAIL_ADDRESS
==========================================

Delete the user by an identifier or an e-mail address.

The parameter ``ID_OR_EMAIL_ADDRESS`` can be either an e-mail address (by pattern)
or a user (unique) identifier.

Response
--------

The result will always be in an empty HTTP-200 response if the user exists.

The result will always be in an empty HTTP-410 response if the user does not exists.