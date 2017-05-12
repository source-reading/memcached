### memcached 配置解读

```json
memcached 1.4.36
-p <num>      TCP port number to listen on (default: 11211)
-U <num>      UDP port number to listen on (default: 11211, 0 is off)
-s <file>     UNIX socket path to listen on (disables network support)
-A            enable ascii "shutdown" command
-a <mask>     access mask for UNIX socket, in octal (default: 0700)
-l <addr>     interface to listen on (default: INADDR_ANY, all addresses)
              <addr> may be specified as host:port. If you don't specify
              a port number, the value you specified with -p or -U is
              used. You may specify multiple addresses separated by comma
              or by using -l multiple times
-d            run as a daemon
-r            maximize core file limit
-u <username> assume identity of <username> (only when run as root)
-m <num>      max memory to use for items in megabytes (default: 64 MB)
-M            return error on memory exhausted (rather than removing items)
-c <num>      max simultaneous connections (default: 1024)
-k            lock down all paged memory.  Note that there is a
              limit on how much memory you may lock.  Trying to
              allocate more than that would fail, so be sure you
              set the limit correctly for the user you started
              the daemon with (not for -u <username> user;
              under sh this is done with 'ulimit -S -l NUM_KB').
-v            verbose (print errors/warnings while in event loop)
-vv           very verbose (also print client commands/reponses)
-vvv          extremely verbose (also print internal state transitions)
-h            print this help and exit
-i            print memcached and libevent license
-V            print version and exit
-P <file>     save PID in <file>, only used with -d option
-f <factor>   chunk size growth factor (default: 1.25)
-n <bytes>    minimum space allocated for key+value+flags (default: 48)
-L            Try to use large memory pages (if available). Increasing
              the memory page size could reduce the number of TLB misses
              and improve the performance. In order to get large pages
              from the OS, memcached will allocate the total item-cache
              in one large chunk.
-D <char>     Use <char> as the delimiter between key prefixes and IDs.
              This is used for per-prefix stats reporting. The default is
              ":" (colon). If this option is specified, stats collection
              is turned on automatically; if not, then it may be turned on
              by sending the "stats detail on" command to the server.
-t <num>      number of threads to use (default: 4)
-R            Maximum number of requests per event, limits the number of
              requests process for a given connection to prevent
              starvation (default: 20)
-C            Disable use of CAS
-b <num>      Set the backlog queue limit (default: 1024)
-B            Binding protocol - one of ascii, binary, or auto (default)
-I            Override the size of each slab page. Adjusts max item size
              (default: 1mb, min: 1k, max: 128m)
-F            Disable flush_all command
-X            Disable stats cachedump and lru_crawler metadump commands
-o            Comma separated list of extended or experimental options
              - maxconns_fast: immediately close new
                connections if over maxconns limit
              - hashpower: An integer multiplier for how large the hash
                table should be. Can be grown at runtime if not big enough.
                Set this based on "STAT hash_power_level" before a
                restart.
              - tail_repair_time: Time in seconds that indicates how long to wait before
                forcefully taking over the LRU tail item whose refcount has leaked.
                Disabled by default; dangerous option.
              - hash_algorithm: The hash table algorithm
                default is jenkins hash. options: jenkins, murmur3
              - lru_crawler: Enable LRU Crawler background thread
              - lru_crawler_sleep: Microseconds to sleep between items
                default is 100.
              - lru_crawler_tocrawl: Max items to crawl per slab per run
                default is 0 (unlimited)
              - lru_maintainer: Enable new LRU system + background thread
              - hot_lru_pct: Pct of slab memory to reserve for hot lru.
                (requires lru_maintainer)
              - warm_lru_pct: Pct of slab memory to reserve for warm lru.
                (requires lru_maintainer)
              - hot_max_age: Items idle longer than this drop from hot lru.
              - cold_max_factor: Items idle longer than cold lru age * this drop from warm.
              - temporary_ttl: TTL's below this use separate LRU, cannot be evicted.
                (requires lru_maintainer)
              - idle_timeout: Timeout for idle connections
              - (EXPERIMENTAL) slab_chunk_max: Maximum slab size. Do not change without extreme care.
              - watcher_logbuf_size: Size in kilobytes of per-watcher write buffer.
              - worker_logbuf_Size: Size in kilobytes of per-worker-thread buffer
                read by background thread. Which is then written to watchers.
              - track_sizes: Enable dynamic reports for 'stats sizes' command.
              - no_inline_ascii_resp: Save up to 24 bytes per item. Small perf hit in ASCII,
                no perf difference in binary protocol. Speeds up sets.
              - modern: Enables 'modern' defaults. Options that will be default in future.
                enables: slab_chunk_max:512k,slab_reassign,slab_automove=1,maxconns_fast,
                         hash_algorithm=murmur3,lru_crawler,lru_maintainer,no_inline_ascii_resp
```
