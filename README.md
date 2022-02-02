# Django Project Config

This empty django project is an example of how to set up some common code quality tools using `pre-commit` and `pre-commit-cli`:

* `black`
* `curlylint`
* `django-browser-reload`
* `django-upgrade`
* `djhtml`
* `editorConfig`
* `flake8` with additional dependencies
* `isort`
* `pre-commit` and `prec-commit-cli`
* `pyupgrade`
* `reorder-python-imports`
* `rich` logging
* `watchman` and `pywatchman`


## Example logging config for `rich` in `settings.py`

```
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'filters': {
        'require_debug_false': {
            '()': 'django.utils.log.RequireDebugFalse',
        },
        'require_debug_true': {
            '()': 'django.utils.log.RequireDebugTrue',
        },
    },
    'formatters': {
        'rich': {'datefmt': '[%X]'},
        'django.server': {
            '()': 'django.utils.log.ServerFormatter',
            'format': '[{server_time}] {message}',
            'style': '{',
        }
    },
    'handlers': {
        'console': {
            'class': 'rich.logging.RichHandler',
            'filters': ['require_debug_true'],
            'formatter': 'rich',
            'level': 'DEBUG',
            'rich_tracebacks': True,
            'tracebacks_show_locals': True,
        },
        'django.server': {
            'level': 'INFO',
            'class': 'logging.StreamHandler',
            'formatter': 'django.server',
        },
        'mail_admins': {
            'level': 'ERROR',
            'filters': ['require_debug_false'],
            'class': 'django.utils.log.AdminEmailHandler'
        }
    },
    'loggers': {
        'django': {
            'handlers': ['console', 'mail_admins'],
            'level': 'INFO',
        },
        'django.server': {
            'handlers': ['django.server'],
            'level': 'INFO',
            'propagate': False,
        },
    }
}
```
