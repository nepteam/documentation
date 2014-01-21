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

More is TBD.