# Setup

You need the command `bear`.

To generate the needed compile_commands.json

```sh
bear make
```

To analyze and thus populate the database:
```sh
dextool mutate analyze --fast-db-store
```

To run the testing:
```sh
dextool mutate test
```

And report!
```sh
dextool mutate report --style html --section summary --section tc_stat --section tc_killed_no_mutants --section tc_unique --section score_history
```

# Config

You probably have to change `build_cmd` to a script (build.sh) that both build
apache httpd and your tests.

If you want more mutants then you need to change the default configuration:

```toml
mutants = ["lcr", "lcrb", "sdl", "uoi", "dcr"]
# to something like
mutants = ["lcr", "lcrb", "sdl", "uoi", "dcr", "aor", "rorp"]
```

It is wise to, if it is possible, to execute your tests in parallel.
This is done by changing:
```toml
test_cmd = [["./test1"], ["./test2"]]
```

The configuration as it is analyze all files but will only mutate those in the
`restrict` section. If you want to further limit the testing you can use the -L
parameter.

```sh
dextool mutate test -Lserver/core.c:50-500
```
