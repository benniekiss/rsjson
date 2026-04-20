# Benchmarks

Benchmarks are in the `bench` folder, and they can be run with the following
commands, where `{iters}` is the number of iterations to run (defaults to
`100`). They use the [`luamark`](https://github.com/jeffzi/luamark) module

```shell
# time benchmarks
lx --lua-version 5.4 lua --test bench/time.lua {iters}

# memory benchmarks
lx --lua-version 5.4 lua --test bench/mem.lua {iters}
```

Here is a comparison between `cjson` and `dkjson` (with the lpeg extension enabled):

Time:

```shell
--------------------
Encoding (Time): 1000 iters
--------------------
pretty=false
  Name     Rank     Relative     Median    Ops  
---------  ----  --------------  ------  -------
cjson        ≈1  █           1x     2ms    500/s
rapidjson    ≈1  █           1x     2ms    500/s
rsjson        3  ██       ↓4.5x     9ms  111.1/s
dkjson        4  ████████  ↓16x    32ms   31.2/s

# NOTE: cjson and rapidjson do not implement pretty formatting
pretty=true
  Name     Rank     Relative      Median   Ops  
---------  ----  ---------------  ------  ------
cjson        ≈1  █            1x     2ms   500/s
rapidjson    ≈1  █            1x     2ms   500/s
rsjson        3  ██        ↓5.5x    11ms  90.9/s
dkjson        4  ████████ ↓17.5x    35ms  28.6/s

--------------------
Decoding (Time): 1000 iters
--------------------
  Name     Rank    Relative       Median      Ops 
---------  ----  ------------  ------------  -----
cjson        ≈1  █         1x           2ms  500/s
rapidjson    ≈1  █         1x           2ms  500/s
rsjson        3  ██████   ↓4x           8ms  125/s
dkjson        4  ████████ ↓5x  10ms ± 500us  100/s
```

Memory:

```shell
--------------------
Encoding (Mem): 1000 iters
--------------------
  Name     Rank     Relative        Median   
---------  ----  ---------------  -----------
cjson         1  ███          1x         13kB
dkjson        2  ██████   ↓1.92x         24kB
rsjson       ≈3  ███████  ↓2.15x  27kB ± 155B
rapidjson    ≈3  ████████ ↓2.29x  29kB ± 17kB

--------------------
Decoding (Mem): 1000 iters
--------------------
  Name     Rank     Relative        Median   
---------  ----  ---------------  -----------
rsjson       ≈1  █            1x   5kB ± 22kB
dkjson       ≈1  ████     ↓2.43x   13kB ± 3kB
rapidjson     3  ███████  ↓4.12x         21kB
cjson         4  ████████ ↓4.61x  24kB ± 880B
```
