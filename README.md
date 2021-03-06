trac-hub
========

**trac-hub** converts [trac](http://trac.edgewall.org/) tickets into github
issues. To this end, it accesses trac's underlying database and copies over
milestones, creates tickets, and replays the change history of each ticket.

Synopsis
--------

Copy the [example YAML configuration](config.yaml.example) and adapt it as
needed:

    cp config.yaml.example config.yaml
    vim config.yaml

Thereafter just invoke `trac-hub`:

    ./trac-hub

By default, trac-hub assumes the file `config.yaml` in the same directory as
the script. You can also specify the configuration file on the command line:

    ./trac-hub -c foo.yaml

Add the `-v` flag for more verbose output:

    ./trac-hub -v

To resume the migration at a given trac ticket ID, use `-s`:

    ./trac-hub -s 42

One can also avoid migration of tickets whose title exists already in the
github issue tracker:

    ./trac-hub -d

*Note*: when converting your trac setup to github, it is prudent to first try
the migration into a test repository which you can delete afterwards. If this
worked out fine and delivered the expected results, one can still aim the
script at the real repository.

Configuration
-------------

The YAML configuration file contains four sections. The section `trac` includes
all trac-related configuration options. At this point trac-hub only supports
SQLite, but it would be trivial to add PostgreSQL and MySQL support.

The section `github` includes the repository to migrate as well as a list of
github account credentials. The latter enables creating issues/comments under
the corresponding github user. If trac-hub cannot map a trac user to a github
user, it defaults to the first account entry. 

The section `labels` allows for custom label mappings. Since github's issue
tracker does not have a first-class notion of ticket priority, type, and
version information, trac-hub supports expressing these in the form of labels. 

The section `users` contains a one-to-one mapping between trac usernames and
github usernames. Each github username must be an authorized collaborator with
push privileges; trac-hub ignores unauthorized mappings.

License
-------

trac-hub comes with a [BSD-style licence](COPYING).
