# JIRA on dotCloud

Deploy JIRA on dotCloud in 60 seconds, thanks to our (un)patented
two-lines "clone-and-push" deployment method:

    git clone git://github.com/jpetazzo/jira-on-dotcloud.git
    dotcloud push jira jira-on-dotcloud

At the end of the push, the URL of your JIRA installation will be shown.
The first start can be a bit slow, so if it does not display at once,
give it a minute to settle down.

## Database configuration

You can test JIRA without a database, by using an "internal" DB.
However, in production environments, you should use an external DB.
In that case, edit the `dotcloud.yml` file and uncomment the
relevant `jiradb` section (you just have two lines to uncomment).
At the end of the push, you will have to use `dotcloud info` to
see the host, port, login and password of the database.

The whole installation process becomes:

    git clone git://github.com/jpetazzo/jira-on-dotcloud.git
    vi jira-on-dotcloud/dotcloud.yml # uncomment the DB you want
    dotcloud push jira jira-on-dotcloud --all
    dotcloud info jira.jiradb

Note tha `--all` flag; it is necessary, because you cloned a
git repository, and by default, dotCloud only pushes committed
changes to the platform.

## Caveat Emptor

This installation of JIRA is not scaled across multiple instances.
It should be pretty reliable, but if you need super high availability,
you should check with dotCloud and/or Atlassian for a more custom,
battle-hardened, setup.
