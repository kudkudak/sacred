Release History
---------------

0.6.3 (2015-04-28)
++++++++++++++++++
* Bugfix: fixed a bug in the mongo observer that would always crash the final
          save
* Bugfix: automatic detection of local source files no longer wrongly detects
          non-local files in subdirectories.

0.6.2 (2015-04-16)
++++++++++++++++++
* Bugfix: fixed crash when using artifacts
* Bugfix: added resources are now saved immediately

0.6.1 (2015-04-05)
++++++++++++++++++
* Bugfix: fixed a crash when some numpy datatypes were not present
          (like numpy.float128)
* Bugfix: Made MissingDependencyMock callable so it would also correctly
          report the missing dependency when called
* Bugfix: MongoObserver would just crash the experiment if the result or the
          info are not serializable. Now it warns and tries to alter
          problematic entries such that they can be stored.

0.6 (2015-03-12)
++++++++++++++++
* Feature: With the new ``add_artifact`` function files can be added to a run
           That will fire an ``artifact event`` and they will also be stored
           in the database by the MongoObserver.
* Feature: Files can be opened through the experiment using ``open_resource``,
           which will fire a ``resource_event`` and the file is automatically
           saved to the database by the MongoObserver
* Feature: Collections used by the MongoObserver can now have a custom prefix
* Feature: MongoObserver saves all sources as separate files to the database
           using GridFS
* Feature: Sources and package dependencies can now also be manually added
* Feature: Automatically collect imported sources and dependencies also from
           ingredients
* Feature: added print_dependencies command
* Feature: With the ``--debug`` flag Sacred now automatically enters
           post-mortem debugging after an exception.
* Feature: Only filter the stacktrace if exception originated outside of Sacred
* Feature: Allow to specify a config file (json, pickle or yaml) on the
           command-line using with.
* Feature: Normal dictionaries can now be added as configuration to experiments
           using the new ``add_config`` method.
* Feature: MongoObserver now tries to reconnect to the MongoDB if connection
           is lost, and at the end of an experiment writes the entry to a
           tempfile if the reconnects failed.
* Bugfix: Invalid config keys could crash the MongoObserver or the
          print_config command. Now they are checked at the beginning and an
          exception is thrown.
* Bugfix: fixed coloring of seeds modified by or entries added by named configs
* Documentation: greatly improved the examples and added them to the docs

0.5.2 (2015-02-09)
++++++++++++++++++
* Bugfix: processor name was not queried correctly on OSX

0.5.1 (2014-10-07)
++++++++++++++++++
* Feature: added special argument ``_config`` for captured functions
* Feature: config entries that remain unchanged through config updates are no
           longer marked as modified by print_config
* Optimization: special arguments ``_rnd`` and ``_seed`` are now only generated
                if needed
* Bugfix: undocumented defective feature ``**config`` removed from
          captured functions
* Bugfix: fixed bug where indentation could lead to errors in a ``ConfigScope``
* Bugfix: added warning when attempting to overwrite an ingredient
          and it is ignored by Sacred
* Bugfix: fixed issue with synchronizing captured out at the end of the run.
          (before up to 10sec of captured output could be lost at the end)
* Bugfix: modifications on seed were not marked correctly by print_config
* Bugfix: changes to seed in NamedConfig would not correctly affect Ingredients
          Note that in order to fix this we removed the access to seed from all
          ConfigScopes. You can still set the seed but you can no longer access
          it from any ConfigScope including named ones.
          (Of course this does not affect captured functions at all.)
* Style: Lots of pep8 and pylint fixes

0.5 (2014-09-22)
++++++++++++++++
* First public release of Sacred