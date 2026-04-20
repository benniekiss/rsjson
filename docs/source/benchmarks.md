# Benchmarks

Benchmarks are in the `bench` folder, and they can be run with the following
commands, where `{iters}` is the number of iterations to run (defaults to
`100`). They use the [`luamark`](https://github.com/jeffzi/luamark) module

```shell
lx add lua-cjson dkjson lpeg luamark

# time benchmarks
lx lua bench/time.lua {iters}

# memory benchmarks
lx lua bench/mem.lua {iters}
```

Here is a comparison between `cjson` and `dkjson` (with the lpeg extension enabled):

Time:

```shell
--------------------
Encoding (Time): 10000 iters
--------------------
pretty=false
 Name   Rank      Relative         Median       Ops  
------  ----  ----------------  -------------  ------
cjson      1  █             1x   12ms ± 500us  83.3/s
rsjson     2  ██        ↓4.42x   53ms ± 500us  18.9/s
dkjson     3  ████████ ↓13.67x  164ms ± 500us   6.1/s

# NOTE: cjson does not have a pretty-print option
pretty=true
 Name   Rank      Relative         Median       Ops  
------  ----  ----------------  -------------  ------
cjson      1  █             1x   12ms ± 500us  83.3/s
rsjson     2  ██        ↓4.92x           59ms  16.9/s
dkjson     3  ████████ ↓15.25x  183ms ± 500us   5.5/s

--------------------
Decoding (Time): 10000 iters
--------------------
 Name   Rank     Relative      Median   Ops  
------  ----  ---------------  ------  ------
cjson      1  █            1x    21ms  47.6/s
rsjson     2  ██████   ↓4.05x    85ms  11.8/s
dkjson     3  ████████ ↓5.14x   108ms   9.3/s
```

Memory:

```shell
--------------------
Encoding (Mem): 10000 iters
--------------------
 Name   Rank     Relative        Median  
------  ----  ---------------  ----------
rsjson     1  █████        1x  13kB ± 4kB
cjson      2  ██████   ↓1.34x        18kB
dkjson     3  ████████ ↓1.54x        21kB

--------------------
Decoding (Mem): 10000 iters
--------------------
 Name   Rank     Relative        Median  
------  ----  ---------------  ----------
dkjson    ≈1  ███████      1x  19kB ± 7kB
cjson     ≈1  ███████  ↓1.02x  20kB ± 9kB
rsjson     3  ████████ ↓1.02x        20kB
```
