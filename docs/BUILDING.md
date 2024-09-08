# Building

## Building for MacOS/Linux

Building PLV8 for MacOS or Linux has some specific requirements:

### Linux

The following packages must be installed to build on Ubuntu or Debian:

- `libtinfo5`
- `build-essential`
- `pkg-config`
- `libstdc++-12-dev` (depending on version, may be 10 instead of 12)
- `cmake`
- `git`

The following packages must be installed to build on EL9 or EL8:

- 'development tools' - via groupinstall
- `cmake`
- `git`

Note that some distributions of Linux may have additional requirements. This
is not meant to be an exhaustive list.

### MacOS

The following packages must be install to build on MacOS:

- `XCode` - and the command line tools
- `cmake`

### Downloading Source

Downloading the source code is very straightforward:

```
$ git clone https://github.com/plv8/plv8
$ cd plv8
$ make
```

### Building

Building is simple:

```
$ make
```

This will download `v8` and compile it as well.

| Note: If you have multiple versions of PostgreSQL installed like 9.5 and 9.6, Plv8 will only be built for PostgreSQL 9.6. This is because make calls pg_config to get the version number, which will always be the latest version installed. If you need to build Plv8 for PostgreSQL 9.5 while you have 9.6 installed pass make the PG_CONFIG variable to your 9.5 version of pg_config. This works for `make`, and `make install`. For example in Ubuntu:

```
$ make PG_CONFIG=/usr/lib/postgresql/13/bin/pg_config
```

### Building with Execution Timeout

Plv8 allows you to optionally build with an execution timeout for Javascript
functions, when enabled at compile-time.

```
$ make EXECUTION_TIMEOUT=1
```

By default, the execution timeout is not compiled, but when configured it has a
timeout of 300 seconds (5 minutes). You can override this by setting the
`plv8.execution_timeout` variable. It can be set between `1` second and `65536`
seconds, but cannot be disabled.

### Installing

Once PLV8 has been built, you need to install it for PostgreSQL to be able to use
it:

```
$ make install
```

This might require `root` access, depending on how PostgreSQL is installed:

```
$ sudo make install
```

### Testing

Once PLV8 is installed, you can verify the install by running:

```
$ make installcheck
```
