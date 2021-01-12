It is a good practice to first execute a dry run.

A dry run does not alter your database.
The database needs to be online, so that Liquigraph can properly detect
which change sets are to be selected (based on whether they already ran, whether they match the execution context ...).

It helps you make sure that:

- your connection settings are correct
- the selected change sets are the ones you expect
