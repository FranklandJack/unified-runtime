PI to UR Migration Guide
########################

As a glue to unify the common code in high level language runtimes Unified
Runtime is designed in part as a replacement for the PI (plugin interface) API used by
the SYCL runtime to support a different backend runtimes. This file documents
the mapping from the PI API objects to their Unified Runtime equivalents and
lays out the migration a developer maintainig a codebase making use of PI would
need to make to switch to Unified Runtime as well as any semantic or syntactic
differences between API objects that are otherwise equivalent.

*API object* in this context refers to either: entry points, types or
enumerations (and their values) defined in the PI/UR headers. For ease of
reference the migration guide is broken into three section for these three
classes of objects.

Entry Points
============

``piPluginInit``
----------------

The PI entry point;

.. code:: c

    __SYCL_EXPORT pi_result piPluginInit(pi_plugin *plugin_info);

has no equivalent entry point in UR.

.. note::

    todo: Write migration guidance

``piPlatformsGet``
------------------

The PI entry point:

.. code:: c

    __SYCL_EXPORT pi_result piPlatformsGet(pi_uint32 num_entries,
                                           pi_platform *platforms,
                                           pi_uint32 *num_platforms);

has been replaced with the following entry point in UR:

.. code:: c

    UR_APIEXPORT zer_result_t UR_APICALL
    urPlatformGet(uint32_t *pCount, ur_platform_handle_t *phPlatforms);


* These APIs have arguments with different semantics. While
  ``piPlatformsGet`` takes an out parameter ``num_platforms`` to report the
  number of registered platforms to the caller, ``urPlatformGet`` takes an
  in/out parameter ``pCount`` which in the special case of being equal to
  zero reports the number of registered platforms to the caller, otherwise
  is an in parameter referring to the number of elements in the
  ``phPlatforms`` array passed by the caller.

.. note::

    todo: Add the remaining entry points

Types
=====

.. note::

    todo: Write this section

Enumerations
============

.. note::

    todo: Write this section
