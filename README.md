# Python Module

The `tldextract` module accurately separates the gTLD and ccTLDs from the
registered domain and subdomains of a URL. For example, you may want the
'www.google' part of [http://www.google.com](http://www.google.com). This is
simple to do by splitting on the '.' and using all but the last split element,
however that will not work for URLs with arbitrary numbers of subdomains and
country codes, unless you know what all country codes look like. Think
[http://forums.bbc.co.uk](http://forums.bbc.co.uk) for example.

`tldextract` can give you the subdomains, domain, and gTLD/ccTLD component of
a URL, because it looks up--and caches locally--the currently living TLDs
according to [iana.org](http://www.iana.org).

    >>> import tldextract
    >>> tldextract.extract('http://forums.news.cnn.com/')
    ExtractResult(subdomain='forums.news', domain='cnn', tld='com')
    >>> tldextract.extract('http://forums.bbc.co.uk/')
    ExtractResult(subdomain='forums', domain='bbc', tld='co.uk')

This module is based on the chosen answer from [this StackOverflow question on
the matter](http://stackoverflow.com/questions/569137/how-to-get-domain-name-from-url/569219#569219).

## Installation

Latest release on PyPI:

    $ pip install tldextract 

Or the latest dev version:

    $ pip install -e git://github.com/john-kurkowski/tldextract.git#egg=tldextract

# Public API

I know it's just one method, but I've needed this functionality in a few
projects and programming languages, so I've uploaded
[`tldextract` to App Engine](http://tldextract.appspot.com/). Just hit it with
your favorite HTTP client with the URL you want parsed like so:

    $ curl "http://tldextract.appspot.com/api/extract?url=http://www.bbc.co.uk/foo/bar/baz.html"
    {"domain": "bbc", "subdomain": "www", "tld": "co.uk"}

