hinance
=======

Continuously scrapes transaction history and current balances from your
banking accounts and stores it in [json](http://www.json.org).

Many banks are supported. Uses [Weboob](http://weboob.org) for scraping.

Low operation costs.
Main supervising process is running continuously on
[Raspberry Pi](http://www.raspberrypi.org).
Scraping jobs are launched from time to time on [AWS](http://aws.amazon.com).

Installation
============

All steps are performed on [Raspberry Pi](http://www.raspberrypi.org).

Install [Docker](http://www.docker.com).

Create directories: `/{etc,var/{lib,tmp}}/hinance-controller`.
There will be sensitive information in `etc` and `tmp` dirs, so it's a good
idea to store them on encrypted volume and make symlinks.

Clone this repo into `/usr/share/hinance-controller/repo`.

Create file `/etc/hinance-controller/config.sh`:

```
AWS_ACCESS_KEY_ID='<<<aws access key id>>>'
AWS_SECRET_ACCESS_KEY='<<<aws secret access key>>>'
AWS_DEFAULT_REGION='us-east-1'
PASSPHRASE='<<<passphrase to encrypt scraped data>>>'
```

Copy your [Weboob](http://weboob.org) `backends` file with banking
accounts into `/etc/hinance-controller`.

Run:

```
/usr/share/hinance-controller/repo/hinance-controller/run.sh \
    2>&1 | logger -p info &
```

Data will be accumulated in `/var/lib/hinance-controller`.

