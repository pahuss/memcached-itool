memcached-itool
===============

The improved memcached-tool on PHP, Python.

New advantages in comparison with default tool are:
* *display* mode shows all slabs not only slabs with keys
* *display* mode also shows percent of wasted memory in chunks
* *dump* mode doesn't trigger deletion of expired keys
* New *removeexp* mode triggers deletion of expired keys
* New *dumpkeys* mode only shows key names
* *dump* and *dumpkeys* modes show expiration status: expired, never expired or how many seconds are left
* New *sizes* mode groups keys by size and shows percent of wasted memory in chunks
* New *settings* mode shows memcached setting during startup

#### Requirements:
PHP 5.3 or
Python 2.6

#### Usage
    python memcached-itool.py <host[:port] | /path/to/socket> [mode]

##### Examples
    python memcached-itool.py localhost:11211 display    # shows slabs information (display is default mode)
    python memcached-itool.py localhost:11211 dumpkeys   # dumps only keys names and their expiration status
    python memcached-itool.py localhost:11211 dump       # dumps keys and values, values only for non expired keys
    python memcached-itool.py localhost:11211 removeexp  # remove expired keys (you may need run several times)
    python memcached-itool.py localhost:11211 settings   # shows memcached settings
    python memcached-itool.py localhost:11211 sizes      # group keys by sizes and show how many we waste memory
    python memcached-itool.py localhost:11211 stats      # shows general stats

*Warning!* dumpkeys, dump, removeexp and sizes modes *will* lock up your cache! It iterates over *every item* and examines the size. 
While the operation is fast, if you have many items you could prevent memcached from serving requests for several seconds.

*Warning!* dump and removeexp modes influence on memcached internal statistic like *expired_unfetched*, *get_hits*, *get_misses* and many others.
So we recommend only use it for debugging purposes.