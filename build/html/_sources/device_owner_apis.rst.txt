Device / Owner APIs
===================

This set of APIs can be called either by the owner of the device or the device itself. However, only the devices which have been registered by their owners with the ``is-autonomous`` header set to ``true``, can call these APIs. Otherwise, their access is restricted only to ``publish`` and ``subscribe`` APIs.

 .. toctree::
    :maxdepth: 1

    follow
    unfollow
    share
    bind
    unbind
    follow_requests
    follow_status
    reject_follow
    permissions


