Usage
=====

This extension defines a custom role called ``:hoverxref:``.
It shows a tooltip when ``hover`` mouse event is triggered,
and populates the content tooltip with the content of the document and section to which the link is pointing.

``:hoverxref:`` uses Sphinx's internals reference resolution to find out where the link points to.
So, the way of referencing the section works in the same way as the ``:ref:`` standard role.

Example:

.. code-block:: rst

   This will :hoverxref:`show a tooltip <hoverxref:section>` in the linked words to ``hoverxref``.

Result:

:hoverxref:`shows a tooltip <hoverxref:section>` in the linked words to ``hoverxref``.


Tooltip on custom object
------------------------

Sphinx has the ability to define custom objects (via `Sphinx.add_object_type`_).
``hoverxref`` can also show a tooltip on these objects if desired.
You need to tell ``hoverxref`` which are the roles where the tooltip has to appear on.
To do this, use :confval:`hoverxref_roles <hoverxref_roles>` config.

Example
~~~~~~~

This documentation defines the ``confval`` role.
The role is used to define all the configurations of the extension.
These configurations are added to the Sphinx index and we can easily refer to them and show a tooltip.
This is reStructuredText code to do this:

.. code-block:: rst

   Show a tooltip to :confval:`hoverxref_auto_ref <hoverxref_auto_ref>` configuration.

the previous code will render to:

Show a tooltip to :confval:`hoverxref_auto_ref <hoverxref_auto_ref>` configuration.


Tooltip on all :ref: roles
--------------------------

If you want to show a tooltip in all the appearances of the ``:ref:`` role,
you have to set the configuration ``hoverxref_auto_ref = True`` in your ``conf.py`` file.

After setting that config, using ``:ref:`` will just render the tooltip:

.. code-block:: rst

   Show a tooltip to :ref:`usage:Tooltip on all :ref: roles` section on this page.

that reStructuredText code will render to:

Show a tooltip to :ref:`usage:Tooltip on all :ref: roles` page.

Tooltip on Sphinx Domains
-------------------------

You can decide whether to use ``hoverxref`` or not on a particular Sphinx Domain as well.

FExample on Python Domain:

.. code-block:: rst

   :py:class:`hoverxref.domains.HoverXRefStandardDomain`

Result:

:py:class:`hoverxref.domains.HoverXRefStandardDomain`


To enable ``hoverxref`` on a domain, you need to use the config :confval:`hoverxref_domains`
indicating which are the domains you desire.


Tooltip with content that needs extra rendering steps
-----------------------------------------------------

Since ``hoverxref`` supports including arbitrary HTML,
you may find that it could be possible that there are some content that it's not well rendered inside the tooltip.
If this is the case, it may be because there are some extra actions that needs to be done after the content is injected in the tooltip.

These actions are usually calling a Javascript function.
``hoverxref`` is prepared to support this type of content and currently supports rendering
`sphinx-tabs`_ and mathjax_.


Example with ``sphinx-tabs``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To render a tooltip with a ``sphinx-tabs`` content you need to enable :confval:`hoverxref_sphinxtabs`.

.. code-block:: rst

   Show a :hoverxref:`tooltip with Sphinx Tabs <installation:Installation>` on its content.

Show a :hoverxref:`tooltip with Sphinx Tabs <installation:Installation>` on its content.


Example with ``mathjax``
~~~~~~~~~~~~~~~~~~~~~~~~

To render a tooltip where its contents has a ``mathjax`` you need to enable :confval:`hoverxref_mathjax`.

.. code-block:: rst

   Show a :hoverxref:`tooltip with Mathjax <mathjax:Mathjax>` formulas.

Show a :hoverxref:`tooltip with Mathjax <mathjax:Mathjax>` formulas.


.. _Sphinx.add_object_type: https://www.sphinx-doc.org/en/master/extdev/appapi.html#sphinx.application.Sphinx.add_object_type

.. _sphinx-tabs: https://github.com/djungelorm/sphinx-tabs
.. _mathjax: http://www.sphinx-doc.org/es/master/usage/extensions/math.html#module-sphinx.ext.mathjax
