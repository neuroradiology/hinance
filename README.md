# hinance

Automated personal bookkeeping for hackers.
For more information please see [homepage](http://www.hinance.org).

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

# Getting Started

Create working directory where all program files will be stored:
```
mkdir <<<my-work-dir>>>
cd <<<my-work-dir>>>
```

Run: `hinance`

It'll generate an empty report in `out/www` folder.
Desktop version is `out/www/dtp-home.html`, mobile - `out/www/mob-home.html`.

Once the report is generated, hit `Ctrl-C` to stop the daemon.

# How It Works

Hinance uses [Weboob](http://weboob.org) to **scrape** data from websites,
**transforms** it into a single consistent bookkeeping journal, and
**generates** the report.

Key point here is that in contrast to other bookkeeping solutions, Hinance
doesn't store an editable database of transactions.
Instead, it transforms immutable set of transactions from the external
websites (banks and shops) into consistent bookkeeping journal.

The user customizes scraping and transformation stages.
On the scraping stage user specifies from which websites does he/she want to
import the data.
On the transformation stage user adds custom transactions categories,
patches imported data, etc.

## Scraping Stage

On this stage Hinance runs Weboob to scrape the data from **banks** and
**shops** websites.
User needs to add corresponding **backends** for each website he/she wants
to import the data from
(please see [Weboob website](http://weboob.org/modules) for the instructions
how to do this).
Weboob modules usable with Hinance must support `CapBank` or `CapShop`
capabilities.
After backends were configured, user must copy config file to the working
hinance directory: `cp ~/.config/weboob/backends in/backends`.

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

Configure [Weboob](http://weboob.org) backends.

Copy weboob backends file: `cp ~/.config/weboob/backends in/backends`

Run: `hinance`

It'll generate the report in `out/www` folder.
Desktop version is `out/www/dtp-home.html`, mobile - `out/www/mob-home.html`.

To exit press `Ctrl-C`.
