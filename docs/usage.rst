=====
Usage
=====

To manage redirect rules navigate to the ``Redirect`` section of the django admin
(usually ``http://www.yoursite.com/admin/djangocms_redirect/redirect``).

For each redirect you must provide:

* **Site**: The site for which you want to add a redirect.
* **Redirect from**: The path that need to be redirected: you can type any URL or select an existing django CMS page.
* **Redirect to**: The path to which the request will be redirected: you can type any URL or select an existing django CMS page.
* **Response code**: You can select 3 types of status_code header: 301 (permanent redirect), 302 (temporary redirect) or 410 (permanent unavailable resource).

Each **redirect from** URL must be unique and start with a slash. If you leave out the
leading slash when creating a redirect, it is added automatically.

If the user requests a page without a trailing slash and there is no redirect for that
URL but there is one for the URL with a trailing slash, that redirect is used. For
backwards-compatibility, this is also true when ``APPEND_SLASH=False``.

If ``APPEND_SLASH=True`` (the default), a trailing slash is added automatically when
creating a redirect. That way, there is only ever a single relevant redirect,
whether there is a trailing slash or not.

****************
Subpath matching
****************

Each redirect can match the exact incoming request path (the default behavior) or a subpath.

Subpath matching comes in two behaviour:

Plain subpath matching
======================

The registered redirects will be checked against the incoming URL and the longest string matching the beginning of the request path will be selected.

The request will be then redirected by replacing the matching **Redirect from** with the **Redirect to** in the original URL.

**Example**

* Incoming request: ``/en/some/path/``
* Redirect from: ``/en/some``
* Redirect to: ``/en/other``
* Resulting redirect: ``/en/other/path/``


Catchall redirect
=================

As in **plain subpath matching** the registered redirects will be checked against the incoming URL and the longest string matching the beginning of the request path will be selected.

The request will be then redirected to the **Redirect to** without further changes.

**Example**

* Incoming request: ``/en/some/path/``
* Redirect from: ``/en/some``
* Redirect to: ``/en/other``
* Resulting redirect: ``/en/other``
