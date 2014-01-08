aldryn-snake
============

Adds tail and head context processors for addons.

Installation
------------

- add ``aldryn_snake.template_api.template_processor`` to your TEMPLATE_CONTEXT_PROCESSORS settings
- somewhere in your app (that will be imported on startup (models, admin etc) add something to the api::

    # -*- coding: utf-8 -*-
    from aldryn_snake.template_api import registry
    from django.conf import settings

    OPTIMIZELY_SCRIPT = """<script src="//cdn.optimizely.com/js/%(account_number)s.js"></script>"""


    def get_crazyegg_script():
      optimizely_number = getattr(settings, 'OPTIMIZELY_ACCOUNT_NUMBER', None)
      if optimizely_number:
          return OPTIMIZELY_SCRIPT % {'account_number': optimizely_number}
       else:
          return ''

    registry.add_to_tail(get_crazyegg_script())

- add the following in your base template to the HEAD::

    {{ TEMPLATE_API_REGISTRY.render_head }}

- add the following in your base template right above </BODY>::

    {{ TEMPLATE_API_REGISTRY.render_tail }}
