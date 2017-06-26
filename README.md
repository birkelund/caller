# caller

Package caller provides a helping hand around runtime.Caller() to look up file,
line and name of the calling function. caller caches the results of its lookups
and strips the uninteresting prefix from both the caller's location and name.

`go get github.com/kbj/caller`

# Usage

By default, the packge assumes that your project files are located on a path
resembling `$GOPATH/src/domain/org/project/(pkg)/module/submodule/file.go`. In
that case, use `caller.Lookup(n)` directly to strip paths down to
`module/submodule/file.go`.

If that does not fit your project, use `caller.NewCallResolver(re
*regexp.Regexp)` in combination with `caller.BuildPathStripper(depth int)` to
get a suitable call resolver. `depth` is the number of subfolders from
`$GOPATH/src` until the root of your project (e.g.
`$GOROOT/src/domain/x/tools/myproject` would be a depth of 3).

# Credits

This package is extracted from the [CockroachDB source
tree](https://github.com/cockroachdb/cockroach/tree/master/pkg/util/caller) and
modified to remove cockroach specific packages.
