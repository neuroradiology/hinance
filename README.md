# hinance

Automated personal bookkeeping for hackers.
For more information please see [homepage](http://www.hinance.org).

# How It Works

Hinance uses [Weboob](http://weboob.org) to scrape data from websites,
transforms it into a single consistent bookkeeping journal, and
generates the report.

Key point here is that in contrast to other bookkeeping solutions, Hinance
doesn't store an editable database of transactions.
Instead, it transforms immutable set of transactions from the external
websites (banks and shops) into human-readable report.
This approach greatly accelerates bookkeeping journal updates,
because once the user has specified the rules for certain class of
transactions, all individual transactions of this kind will be handled
automatically.

User controls scraping and transformation stages. On scraping stage user
specifies from which websites does he/she wants to import the data.
On the next stage user adjusts transformation process by adding custom
transactions categories, patching imported data, etc.

# Installation

There's a [package](https://aur.archlinux.org/packages/hinance) for Arch Linux.

There's also a reproducible Dockerized
[build automation](https://github.com/hinance/www) for the project homepage,
which includes all the necessary dependencies.
The Docker container is pre-built and uploaded to the repository, but if you
want to build it yourself, keep in mind that it takes about 1 hour on 4 cores,
8GB RAM machine.

Feel free to use the above as a reference when installing on your target
platform.

# Usage

Create working directory where all program files will be stored:
```
mkdir <<<my-work-dir>>>
cd <<<my-work-dir>>>
```

Copy and edit customization files (see next sections for details):
```
cp -r /usr/lib/hinance/default in
vim config.sh
vim user_tag.hs
vim user_data.hs
```

Configure [Weboob](http://weboob.org) backends. These are the websites
you want to import the data from. Bank modules must support `CapBank`
capability, shop modules - `CapShop`. See [Weboob website](http://weboob.org)
for more info.

Run: `hinance`

It'll generate the report in `out/www` folder.
Desktop version is `out/www/dtp-home.html`, mobile - `out/www/mob-home.html`.

To exit press `Ctrl-C`.
