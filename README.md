# gh-subscriptions: very basic tool for managing GitHub repo subscriptions

This is a very basic tool intended to stop watching a large number of GitHub
repos.

**Use at your own risk!**

## Set up

You must have Python and `pip` installed.  I used Python 3.4.3.

First, install PyGithub to your local user directory:

    pip install --user PyGithub

You should be able to leave off `--user` if you have permissions to install
globally and would prefer that.

Now, [generate a GitHub Personal Access Token](https://github.com/settings/tokens)
with permissions on the scope `repo`.  You can label the token (e.g.,
"gh-subscriptions tool").  Copy the token into a local file called
`github-access-token`.  This must be in your working directory when you run this
tool.

Now you can list repositories that you're watching:

    $ ./gh-subscriptions list
    davepacheco/kartlytics
    davepacheco/mdb_v8
    ...

You can remove yourself from a list of repositories by listing them in a file
(one repository per line) and using:

    $ ./gh-subscriptions remove-from-file to-remove.txt

By default, this will just print out what it would do.  To actually stop
watching them, use:

    $ ./gh-subscriptions remove-from-file -f to-remove.txt

## Putting it together

If you want to stop watching a lot of repositories, try something like this:

    # List all the repositories that you're watching:
    $ ./gh-subscriptions list | sort > all-repos.txt

    # Edit the list to include only the repos you want to stop watching:
    $ cp all-repos.txt to-remove.txt
    $ vim to-remove.txt

    # Hand-check the output:
    $ ./gh-subscriptions remove-from-file to-remove.txt

    # Finally, stop watching the repos:
    $ ./gh-subscriptions remove-from-file -f to-remove.txt

## Known issues

For some reason I have not yet debugged, the tool does not seem to successfully
unwatch all repos that you ask it to, nor does it report a problem.  However,
you can re-run the command and it will unwatch some of the ones it missed last
time.

## See also

* [PyGithub](https://github.com/PyGithub/PyGithub): module used for accessing
  GitHub.  Also see [PyGithub
  documentation](https://pygithub.readthedocs.io/en/latest/introduction.html).
* GitHub API documentation for [listing repositories being watched](https://developer.github.com/v3/activity/watching/#list-repositories-being-watched) and [stopping watching a repository](https://developer.github.com/v3/activity/watching/#stop-watching-a-repository-legacy).
* [Manage your GitHub Personal Access
  Tokens](https://github.com/settings/tokens)
