#############################
Ansible modules for Syncthing
#############################

This is a small collection of modules that use the JSON API of the Syncthing client. Use at your own risk!

Overview
********

Dependencies / expected environment
***********************************

Authentication
**************
Authentication is performed using an API key that is unique to each instance of Syncthing. The key can be viewed in
the web-gui or in the config file. If you're running the modules on the host syncthing runs on, the api key can be
extracted using the following ansible-snippet:

.. code-block:: yaml

   ---
   - name: Extract the key from the config file
     xml:
       path: /path/to/syncthing/config.xml
       xpath: /configuration/gui/apikey
       content: text
     register: _api_key

   - set_fact:
       api_key: "{{ _key.matches[0].apikey }}"

   - debug:
       msg: "API Key: {{ api_key }}"

Modules
*******
All modules use the following variables to connect:

* ``address`` is the address the syncthing client listens on (defaults to ``localhost``)
* ``port`` is the syncthing port, defaults to ``8384``.
* ``apikey`` is the api key set in syncthing

