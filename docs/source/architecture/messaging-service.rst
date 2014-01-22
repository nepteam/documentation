Messaging Service
#################

.. blockdiag::

    blockdiag {
        MessagingService -> WebService
        MessagingService -> AMQP
        MessagingService -> Cache
    }

The message is packaged in an encrypted JSON-formatted data.

This is to allow three operations.

- Push notification (single-way communication)
- Data synchronization (two-way communication)
- Chat service

More is TBD.