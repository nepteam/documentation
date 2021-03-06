Data Classification
###################

.. contents:: Table of Contents

.. note::

    Property **created** and **updated** are not editable or manually defined.
    **created** is **only** assigned automatically by the web service upon the
    creation of entity. However, **updated** is **always** updated automatically
    by the web service upon any updates of the entity.

User class
==========

This represents the user. It is a security class.

.. code-block:: python

    class User:
        name # str (unicode)
        alias # str (alphanumeric only)
        email # str
        password # str
        salt # str
        created # float (unix timestamp)
        updated # float (unix timestamp)

.. note::

    In the initial prototype phase, only **name**, **alias** and **email** are used.
    
.. warning::

    Only *alias*, *email* and *salt* should be read-only after the user creation
    (or registration).

Ticket class
============

It is an electronic pass for a user to participate only one session (Session).

The *role* of the ticket will determine what the user can do in a particular
session. For instance, an *observer* may only see some data, like and the overall
statistic data and the current set of responses at a certain time. In meanwhile,
*attendee*s can only respond to the *guided* sequence.

.. code-block:: python

    class Ticket:
        user # security.User
        role # ENUM['observer', 'attendee']
        session # Session
        status # ENUM['valid', 'using', 'used', 'void']
        created # float (unix timestamp)
        updated # float (unix timestamp)

.. note::

    For the sake of data integrity, only **status** is changeable.

Session class
=============

It represents a group session, e.g., class session, seminar session, examination
session etc.

It must have at least one *tags* for query, classification and fast access.

.. code-block:: python

    class Session:
        name # str
        tags # list<str>
        owner # security.User
        end_reason # ENUM[None, 'done', 'postponed', 'cancelled', 'technical_difficulty']
        is_active # bool
        is_public # bool
        collection # Collection
        started # float (unix timestamp)
        finished # float (unix timestamp)
        created # float (unix timestamp)
        updated # float (unix timestamp)

Collection class
================

It represents a collection of sequences (e.g., topic, chapter etc.).

It must have at least one *tags* for query, classification and fast access.

.. code-block:: python

    class Collection:
        name # str
        tags # list<str>
        created # float (unix timestamp)
        updated # float (unix timestamp)

Sequence class
==============

It represents a sequence, question (normal or survey) or test.

It must have at least one *tags* for query, classification, fast access and data
analysis.

Its *priority* should automatically be determined by the interface. Manual
manipulation on this property should be reserved for emergency only.

.. code-block:: python

    class Sequence:
        title # str
        detail # str
        tags # list<str>
        priority # float
        collection # Collection (many-to-one)
        created # float (unix timestamp)
        updated # float (unix timestamp)

.. note::

    When the sequence has no options, the system will automatically determine
    that this sequence requires a written response, instead of multiple choices.

.. note::

    When the project exits the prototype phase, we will either extend this class
    to support just a presentation data, questions, survey and test.

Option class
============

It represents an option of a particular sequence.

It must have at least one *tags* for query, classification, fast access and data
analysis.

Its *note* is used for clarifying the meaning or intention of the option.

Its *value* is used for data analysis. It could be used to analyze along with *tags*.

.. code-block:: python

    class Option:
        name # str
        note # str
        tags # list<str>
        sequence # Sequence (many-to-one)
        value # int
        created # float (unix timestamp)
        updated # float (unix timestamp)

Response class
==============

It represents a user response to the sequence in a particular session.

The *text* is used only when the sequence requires a written response.

.. code-block:: python

    class Response:
        ticket # Ticket (many-to-one)
        sequence # Sequence (many-to-one)
        option # Option (many-to-one)
        text # str
        created # float (unix timestamp)

.. note:: This class does not have the timestamp for update.
