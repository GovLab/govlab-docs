# Common Issues and Solutions

## Issue
When deploying receive an error similar to this:

```
[13:50:59] Error in plugin 'gulp-gh-pages'
Message:
    ENOENT: no such file or directory, open '.publish/.git/HEAD'
Details:
    errno: -2
    code: ENOENT
    syscall: open
    path: .publish/.git/HEAD
```

## Solution
run `rm -rf .publish` and try to deploy again