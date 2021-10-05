# gcl-bt-collision

Imagine you have some files in your project with a particular build tag you want to lint, for example, `gofuzz` 
(see fuzz.go).

In order to accomplish the above statement, you add the mentioned tag to the run section of the `.golangci.yml` file.

It also happens that one of your dependencies is using the same build tag inside their codebase 
(github.com/pion/dtls/v2).

Apparently those build tags collide somehow, so `golangci-lint` would fail with the following err:

```
WARN [runner] Can't run linter goanalysis_metalinter: buildir: failed to load package dtls: could not load export data: no export data for "github.com/pion/dtls/v2" 
```

This apparently inoffensive warning breaks the `golangci-lint run ./...` preventing other files from being linted.