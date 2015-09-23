### Skip using this

See [Spook](https://github.com/johnae/spook) instead.


### Poor mans guard: sentry

This is a very simple tool with some of the functionality of guard: https://github.com/guard/guard

It's meant to be lightweight and simple to use without too many bells and whistles. What it CAN do is enable the same code/test/repeat feedback loop as guard gives, namely: edit and save your code to disk and watch the specs for that file run.

It's using a naive approach currently where it simply looks for a file in the spec dir called:

```
dirname-of-the-file-with-code/name-of-file-with-code_spec.*
```

In practice this has worked on a few projects for me but ymmv. For this to work it's absolutely essential that you install the entr command, see http://entrproject.org or https://bitbucket.org/eradman/entr/commits/all. This project wouldn't be possible at all without entr.

## Installing sentry

The easiest way to install sentry is probably by doing this:

```
curl https://raw.githubusercontent.com/johnae/sentry/master/install | sudo bash
```

The easiest way to uninstall it is probably by doing this:

```
curl https://raw.githubusercontent.com/johnae/sentry/master/uninstall | sudo bash
```

However, if you don't like running scripts from the internet as root blindly, you can clone this repo and copy everything in bin/ to somewhere in your PATH. Or you can take a look at the install script which is pretty straightforward.

Please remember, you must install entr for it to work. You will be notified about this during the installation as well as if you try to run it without having entr installed.

## Running sentry

If you are in a rails project, you might run it like this (from within the project directory).

```
sentry watch rspec -f d
```

The default watch dirs are:

src/
lib
app/
spec/
test/

You may add additional watch dirs by creating a file in your project directory called .sentry and add dirs like this:

SENTRY_WATCH_DIRS="mysrc mylib"

Those will be appended to the defaults. Only dirs that exist will actually be watched.

## More configuration

There is very basic mapping capability through .sentry_mapping - a file in your project dir. It is expected to contain:

```
spec/path/file_spec.ext app/path/somecode.ext
spec/path/other_spec.ext app/path/*/stuff_*.ext
```

