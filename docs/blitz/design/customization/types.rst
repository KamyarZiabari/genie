.. _types:


Creating a custom action
^^^^^^^^^^^^^^^^^^^^^^^^

The structure needed to create a custom action in *Blitz* is pretty straight forward. A new module (e.g. customBlitz.py) with a new class
should be created. Within the said class, *Blitz* class should be inherited and the action can be developed. The content of that action can be anything that helps users
with their testing. Look at example below

.. code-block:: PYTHON

  import logging
  from pyats import aetest
  from genie.libs.sdk.triggers.blitz.blitz #import Blitz


  log = logging.getLogger()

  class CustomBlitz(Blitz):  # <- inheriting Blitz
    def my_custom_action(self, steps, device. **kwargs):
      log.info("This is my custom action")


Later on the custom action can be called within the trigger datafile, with the same name as the function name.

.. code-block:: YAML

  TestCustomAction:
      source:
        pkg: CustomBlitz
        class: <path_to_custom_blitz_class>
      devices: ['uut']
      test_sections:
          - section_name:
            - my_custom_action:
              device: PE1
              key1: val1
              key2: val2

Creating a custom section
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The behavior of a *Blitz* section also can be customized. Just like custom actions, to create a customized section, a class that inherits *Blitz* class should be created.
A function that represent the custom section should be created within said class and be decorated with ``@aetest.test``. Look  at the below example.


.. code-block:: PYTHON

  import logging
  from pyats import aetest
  from genie.libs.sdk.triggers.blitz.blitz #import Blitz


  log = logging.getLogger()

  class CustomBlitz(Blitz):  # <- inheriting Blitz
    @aetest.test
    def my_custom_section(self, steps, testbed, data):
      log.info("This is my custom section")



.. code-block:: YAML

  TestCustomAction:
      source:
        pkg: CustomBlitz
        class: <path_to_custom_blitz_class>
      devices: ['uut']
      test_sections:
          - my_custom_section:
            - my_custom_action:
              device: PE1
              key1: val1
              key2: val2
