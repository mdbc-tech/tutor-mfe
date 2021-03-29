Micro frontend base plugin for `Tutor <https://docs.tutor.overhang.io>`__
=========================================================================

⚠️ THIS IS A WORK-IN-PROGRESS NOT READY FOR RELEASE JUST YET


This plugin is required to run other `micro frontends (MFEs) <https://edx.readthedocs.io/projects/edx-developer-docs/en/latest/all_development/common_tech/micro_frontends.html>`__ with Tutor.

TODO
----

- Get rid of all TODOs
- Make sure that it works with other MFEs
- re-build the mfe docker image on init/start
- Fix CORS issues caused by fonts downloads from Google in Profile MFE
- Get this to work in development
- Get this to work in Kubernetes
- Write some docs!

Installation
------------

::

    pip install tutor-mfe

Usage
-----

::

    tutor plugins enable mfe


TODO: provide a quick one-line commands for adding values to site config?
To enable the account MFE, `ENABLE_ACCOUNT_MICROFRONTEND` must be added to the site configuration.
To enable the profile MFE, `ENABLE_PROFILE_MICROFRONTEND` must be added to the site configuration.

TODO explain how to disable individual MFEs.

Gradebook
~~~~~~~~~

Follow the Open edX documentation on enabling the Gradebook: https://github.com/edx/frontend-app-gradebook/#configuring-for-local-use-in-edx-platform The settings do not need to be modified, but you will need to enable several waffle flags and switches.


License
-------

This software is licensed under the terms of the AGPLv3.
