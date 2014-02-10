Toolshed: ``ink``
---------------------------------

.. py:module:: Naked.toolshed.ink


Import Ink Module
^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.ink


Import Ink C Module
^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.c.ink

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^

The Ink module contains two classes for text templating.   The Ink templating syntax is very flexible, allowing you to assign the replacement tag delimiters that you would like to use.  The default opening delimiter is ``{{`` and the default closing delimiter is ``}}``.

This allows you to perform replacements in a string such as:

.. code-block:: python

    template_string = "{{name}} is {{attribute}}"

with values from a Python dictionary where the dictionary keys are mapped to the tag name inside the opening and closing delimiters:

.. code-block:: python

    replacement_dict = {'name': 'Naked', 'attribute': 'neat'}

Dictionary values are replaced at every position where a matching replacement tag is identified in the string.

The :py:class:`Template` class is used to create instances of Ink template strings and the :py:class:`Renderer` class is used to execute the text replacements in a :py:class:`Template` instance.

Classes
^^^^^^^^

.. py:class:: Template(template_text [, open_delimiter="{{"] [, close_delimiter="}}"] [, escape_regex=False])

    The Template class is an extension of the Python string type and you can use any string method on a Template instance.  An instance of the Template class is constructed with a string that contains the template text.  You have the option to indicate different opening ``open_delimiter`` and closing ``close_delimiter`` delimiters as arguments to the constructor if your template uses different characters.  If you use special regular expression characters as delimiters, include an ``escape_regex=True`` argument.

    .. note::

        The need to escape special regular expression characters slows the construction of each instance of a Template.  This will not significantly influence the running time of your application if you are creating a relatively small number of Template instances.  Perform testing to confirm that this does not become significant if you are generating a large number of Template instances with special regular expression character delimiters.  This does not apply to the default Ink template delimiters.

    There are no public methods for the ``Template`` class.

.. py:class:: Renderer(Template, key [, html_entities=False])

    The Renderer class takes a :py:class:`Template` argument and a Python dictionary ``key`` argument.  You have the option to escape HTML entities in the replacement text (i.e. the values contained in the Python dictionary ``key``) by setting ``html_entities=True`` on construction of a new Renderer instance.

    Dictionary keys are mapped to the replacement tag names (i.e. the string between the replacement delimiters) in the Template and the dictionary values are the strings that are used for text replacements at *every* matching replacement tag position in the Template.

    .. py:method:: render()

        The render() method executes text replacements in the Template instance that was passed as an argument to the Renderer constructor using the key:value mapping in the dictionary that was passed as an argument to the Renderer constructor (see example below).


Examples
^^^^^^^^^
**Create an Ink Template with Default Delimiters**

.. code-block:: python

    from Naked.toolshed.ink import Template

    template_string = "I like {{food}} and {{drink}}"
    template = Template(template_string)

**Create an Ink Template and Specify New Delimiters**

.. code-block:: python

    from Naked.toolshed.ink import Template

    template_string = "I like [[food]] and [[drink]]"
    template = Template(template_string, open_delimiter="[[", close_delimiter="]]", escape_regex=True)

**Render an Ink Template**

.. code-block:: python

    from Naked.toolshed.ink import Template, Renderer

    template_string = "I like {{food}} and {{drink}}"
    template = Template(template_string)
    template_key = {'food': 'fries', 'drink': 'beer'}
    renderer = Renderer(template, template_key)
    rendered_text = renderer.render()
    print(rendered_text)         # prints "I like fries and beer"


