Messaging Service
#################

.. blockdiag::

    blockdiag {
        MessagingService -> WebService
        MessagingService -> AMQP
        MessagingService -> Cache
    }

Prerequisite
============

- RabbitMQ
- Tori Framework / Tornado Framework (for WebSocket)

More is TBD.