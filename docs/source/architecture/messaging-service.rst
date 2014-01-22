Messaging Service
#################

.. blockdiag::

    blockdiag {
        MessagingService -> WebService
        MessagingService -> AMQP
        MessagingService -> Cache
    }

The message is packaged in an encrypted JSON-formatted data.

This is to allow four operations.

- Push notification
- Data synchronization (TBD)
- Chat service (TBD)
- Remote control service

Prerequisite
************

- Python*
- Tori Framework / Tornado Framework (for WebSocket)
- Pika
- RabbitMQ
- MySQL

.. note::

    We currently aim for Python 2.7.x until Pika supports Python 3.3 or higher.

More is TBD.