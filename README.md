# genhost

This script will randomly generate hostnames by picking words from the provided
word list. The pool of words comes from Oren Tirosh's [mnemonic encoding][]
project.

[mnemonic encoding]:
  http://web.archive.org/web/20090918202746/http://tothink.com/mnemonic/wordlist.html

## Usage

Just run the script and provide the number of hostnames you'd like to generate:

    $ ./genhost 4
    romeo.example.com
    holiday.example.com
    jester.example.com
    spiral.example.com

All of those words will automatically be commented out in the word list and thus
removed from the pool of future names. If a hostname has the potential to be
confusing based on technical jargon (like `email.example.com`), simply ignore it
and generate a replacement.

If you decommission a server, you can return its hostname to the usable pool,
thereby uncommenting it in the wordlist:

    $ ./genhost reuse jester

You can also print a list of the hostnames currently marked as in use:

    $ ./genhost list
    romeo
    holiday
    spiral

For collaboration purposes, don't forget to commit the updated word list back to
a shared Git repository so names do not get reused:

    $ git add wordlist
    $ git commit
    $ git push

### Environment Variables
| Variable | Description | Default |
|----------|-------------|---------|
| `GENHOST_DOMAIN` | The domain name to append to generated hostnames | example.com |
| `GENHOST_WORDLIST` | Filename of the word list to use, relative to genhost directory | wordlist |

    $ export GENHOST_DOMAIN=github.com
    $ ./genhost 3
    cover.github.com
    kilo.github.com
    open.github.com

    $ export GENHOST_WORDLIST=colors.txt
    $ ./genhost 1
    yellow.github.com
