Web Service
###########

.. contents::

How it normally works
*********************

The API will be implemented as JSON RPC.

Please note that all requests to the API will require an **application access
token set** which only the web interface (only via a user with the **master
permit**) or the command line interface can manage the token.

The API will always expect all incoming requests to have a header **X-EWSAPI-TOKEN**
with an **application access token set**.

If the application access token set is not present or invalid, the service will
return an empty **HTTP-403** response.

If not specified, a **HTTP-500** response is returned. It is empty if only the
debugging mode is disabled.

.. note::

    In the early stage of development, the usage of application access token sets
    will not be enforced.
