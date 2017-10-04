git-client
==========

This role installs git client with my preferred settings and attributes. It includes send-mail, gpg (gnupg2) and gerrit settings.

The git templates contain a pre-commit hook for all your new projects when you run `git init`. This pre-commit hook runs pep8, pylint and pyflakes on all `*py` files you commit.

See [files/pre-commit](files/pre-commit) for more details.

Requirements
------------

This role assumes you have previously installed:

* vim (my git preferred editor)
* gnupg2 and you have created your private key

It also assumes that the user's directory to which the `homedir` is set to has been previously configured.

For example, my machines are configured to have my username set to *tmoreira*. Therefore, if I want to run this role to install git-client to my username then I will set the `homedir` variable to

```yaml
homedir: '/home/tmoreira'
```

The pre-commit hook script assumes you have  PEP8, PyLint and PyFlakes installed.


Role Variables
--------------

```yaml
homedir: '/home/foo'                # git templates will be installed at:
                                    #     {{ homedir }} /.git_templates
git:
  user:                             # general git client user's settings
    name: 'Foo'                     # user's full name
    email: 'foo@example.com'        # user's email
    signingkey: '01234567'          # user's GPG key

  sendemail:                        # settings used by git-email
    smtpuser: 'yourname@gmail.com'  # smtp server username
    smtpserver: 'smtp.gmail.com'    # smtp server address
    smtpserverport: '587'           # smtp server port (OPTIONAL)
    smtpencryption: 'tls'           # smtp encryption (OPTIONAL)

  gitreview:                        # settings used by git-review
    username: 'foo'                 # user's gerrit username
```

Playbook Example
----------------

```yaml
    - hosts: servers
      roles:
         - git-client
```

License
-------

GPLv3

Author Information
------------------

Tiago M. Vieira - https://github.com/tvieira
