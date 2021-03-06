Time Entry
==========

Supported by Redmine starting from version 1.1

Manager
-------

All operations on the time entry resource are provided via it's manager. To get
access to it you have to call ``redmine.time_entry`` where ``redmine`` is a configured
redmine object. See the :doc:`../configuration` about how to configure redmine object.

Create methods
--------------

create
++++++

.. py:method:: create(**fields)
    :module: redmine.managers.ResourceManager
    :noindex:

    Creates new time entry resource with given fields and saves it to the Redmine.

    :param integer issue_id or project_id: (required). The issue id or project id to log time on.
    :param integer hours: (required). The number of spent hours.
    :param string spent_on: (optional). The date the time was spent (current date if not set).
    :param integer activity_id: (optional). The id of the time activity. This parameter is required unless
      a default activity is defined in Redmine.
    :param string comments: (optional). Short description for the entry (255 characters max).
    :return: TimeEntry resource object

.. code-block:: python

    >>> time_entry = redmine.time_entry.create(issue_id=123, spent_on='2014-01-14', hours=3, activity_id=10, comments='hello')
    >>> time_entry
    <redmine.resources.TimeEntry #12345>

new
+++

.. py:method:: new()
    :module: redmine.managers.ResourceManager
    :noindex:

    Creates new empty time entry resource but doesn't save it to the Redmine. This is useful
    if you want to set some resource fields later based on some condition(s) and only after
    that save it to the Redmine. Valid attributes are the same as for ``create`` method above.

    :return: TimeEntry resource object

.. code-block:: python

    >>> time_entry = redmine.time_entry.new()
    >>> time_entry.issue_id = 123
    >>> time_entry.spent_on = '2014-01-14'
    >>> time_entry.hours = 3
    >>> time_entry.activity_id = 10
    >>> time_entry.comments = 'hello'
    >>> time_entry.save()
    True

Read methods
------------

get
+++

.. py:method:: get(resource_id)
    :module: redmine.managers.ResourceManager
    :noindex:

    Returns single time entry resource from the Redmine by it's id.

    :param integer resource_id: (required). Id of the time entry.
    :return: TimeEntry resource object

.. code-block:: python

    >>> time_entry = redmine.time_entry.get(374)
    >>> time_entry
    <redmine.resources.TimeEntry #374>

all
+++

.. py:method:: all(**params)
    :module: redmine.managers.ResourceManager
    :noindex:

    Returns all time entry resources from the Redmine.

    :param integer limit: (optional). How much resources to return.
    :param integer offset: (optional). Starting from what resource to return the other resources.
    :return: ResourceSet object

.. code-block:: python

    >>> time_entries = redmine.time_entry.all(offset=10, limit=100)
    >>> time_entries
    <redmine.resultsets.ResourceSet object with TimeEntry resources>

filter
++++++

.. py:method:: filter(**filters)
    :module: redmine.managers.ResourceManager
    :noindex:

    Returns time entry resources that match the given lookup parameters.

    :param project_id: (optional). Get time entries from the project with the given id.
    :type project_id: integer or string
    :param integer issue_id: (optional). Get time entries from the issue with the given id.
    :param integer user_id: (optional). Get time entries for the user with the given id.
    :param string spent_on: (optional). Date when hours was spent (for Redmine >= 2.3.0).
    :param string from_date: (optional). Limit time entries from this date.
    :param string to_date: (optional). Limit time entries until this date.
    :param string hours: (optional). Get only time entries that are =, >=, <= hours.
    :param integer limit: (optional). How much resources to return.
    :param integer offset: (optional). Starting from what resource to return the other resources.
    :return: ResourceSet object

.. code-block:: python

    >>> time_entries = redmine.time_entry.filter(offset=10, limit=100, project_id='vacation', hours='>=8')
    >>> time_entries
    <redmine.resultsets.ResourceSet object with TimeEntry resources>

.. hint::

    You can also get time entries from an issue resource object directly using
    ``time_entries`` relation:

    .. code-block:: python

        >>> issue = redmine.issue.get(34213)
        >>> issue.time_entries
        <redmine.resultsets.ResourceSet object with TimeEntry resources>

Update methods
--------------

Not yet supported by Python Redmine

Delete methods
--------------

delete
++++++

.. py:method:: delete(resource_id)
    :module: redmine.managers.ResourceManager
    :noindex:

    Deletes single time entry resource from the Redmine by it's id.

    :param integer resource_id: (required). Time entry id.
    :return: True

.. code-block:: python

    >>> redmine.time_entry.delete(1)
    True
