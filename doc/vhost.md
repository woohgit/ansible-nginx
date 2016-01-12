Vhost management
================

You can see many examples in: [tests/test.yml](../tests/test.yml).

`nginx_vhosts`: List of dict. A vhost has few keys. See bellow.

Common
------

  - `name`: (M) Domain or list of domain used.
  - `template`: (D) template used to create vhost. Optional if you set `delete` to true or using `redirect_tor`.
  - `enable`: (O) Enable the vhost (default is true)
  - `delete`: (O) Delete the vhost (default is false)
  - `redirect_from`: (O) Domain list to redirect to the first `name`. You can use this key to redirect non-www to www
  - `redirect_to`: (O) Redirect all requests to this domain. Please set scheme (http:// or https:// or $sheme).
  - `redirect_to_code`: Redirect code (default: 302)
  - `location`: (O) Add new custom locations (it does not overwrite!)
  - `more`: (O) Add more custom infos.
  - `upstream_params`: (O) Add upstream params (useful when you want to pass variables to PHP)
  - `override_try_files`: (O) overrides default try\_files defined in template
  - `manage_local_content`: (O) Boolean. Set to false if you do not want to manage local content (images, css...). This option is useless if you use `_proxy` template or `redirect_to` feature.
  - `htpasswd`: (0) References name key in `nginx_htpasswd`. Enable auth basic on all vhost.

(O): Optional
(M): Mandatory
(D): Depends other keys...

Templates
---------

  - `_base`: static template
  - `_backuppc`: access to [BackupPC](http://backuppc.sourceforge.net/) (be careful: you need to install [fcgiwrap](https://packages.debian.org/jessie/fcgiwrap))
  - `_dokuwiki`
  - `_redirect`: should not be called explicitly
  - `_phalcon`: Phalcon PHP Framework
  - `_php`: PHP base template. Can work with many frameworks/tools
  - `_php_index`: Same as above. But you can only run index.php
  - `_proxy`
  - `_wordpress`

Templates works as parent-child.

About proxy template
--------------------

Proxy template allow you to use Nginx as reverse proxy. Usefull when you have an application service such as Redmine, Jenkins...

You have many key added to vhost key:

  - `upstream_name`: (O) upstream name used to pass proxy
  - `proxy_params`: (M) list of raw params passed to the vhost

(O) : Optional
