Sometimes you know that code was broken, but you have no idea who broke and
when it was broken. For finding answers to those questions, there are few
tools that help getting closer to the root of the problem.

Or maybe you're just curious what you did last summer.

# easiest case, you're culprit and code worked moment ago

- it's good habit of making a commit when code works

- if you do that, you can run git diff and start comparing what changed

- having unit tests helps a lot as ideally they're quick to run and you can
  even make a hook, so they're run before commit is made

# browsing logs

- this method needs good quality commit messages

- also if people have habit of bundling unrelated changes into commits that are
  not mentioned in the commit message, things get more difficult

## filtering logs

- git can get logs for invidual files, it's as simple as giving filename as
  parameter (put -- before the filename if want logs about file that no longer
  exists)

- if you know who to blame, --author might come handy

- if you remember part of commit message use --grep

- if you are interested in when certain line was changed, explore -G

- actually very handy especially you're trying to figure out when a line was
  removed

# figuring out where the line came from

- sometimes some line in the code looks odd and you wonder what's the original
  context where it came from

- maybe the line made sense earlier in the original context

- git blame helps figuring that out

- also as name implies, it's also very handy tool for blaming people if you
  really want to do that

- if lines were recently copied or moved, exploring -C and -M might be
  worthwhile
 
- exploring -w might be worthwhile as that ignores whitespace changes

# testing the code

- git bisect comes very handy if you know when code worked and when it was
  broken (usually the latest commit) and log browsing doesn't seem to help

- git bisect is tool that can be used to hunt down the commit where the bug was
  introduced by testing the code and telling the result to git bisect either
  manually or in automated fashion

- git bisect speeds up by using binary search, so all commits don't have to be
  tested

- git bisect can also run shell script and determine the test result from the
  exit code

# avoiding problems - the Git way

- Git has kind of automation feature that's called hooks

- with that it's possible to hook code (or shell script to be more exact) into
  to be run before after Git operations

- that can be used for things like running static analysis tools before commit
  is created

- server side hooks also exist

- there's plenty of samples created by `git init` available from .git/hooks
