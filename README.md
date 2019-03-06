[![Release](https://img.shields.io/github/release/llorllale/go-gitlint.svg?style=flat-square)](https://github.com/llorllale/go-gitlint/releases/latest)
[![Build Status](https://travis-ci.org/llorllale/go-gitlint.svg?branch=master)](https://travis-ci.org/llorllale/go-gitlint)
[![codecov](https://codecov.io/gh/llorllale/go-gitlint/branch/master/graph/badge.svg)](https://codecov.io/gh/llorllale/go-gitlint)
[![Go Report Card](https://goreportcard.com/badge/github.com/llorllale/go-gitlint?style=flat-square)](https://goreportcard.com/report/github.com/llorllale/go-gitlint)
[![codebeat](https://codebeat.co/badges/16512202-9758-4e2e-b0b8-4121724680b8)](https://codebeat.co/projects/github-com-llorllale-go-gitlint-master)
[![GolangCI](https://golangci.com/badges/github.com/llorllale/go-gitlint.svg)](https://golangci.com/r/github.com/llorllale/go-gitlint)
[![Powered By: GoReleaser](https://img.shields.io/badge/powered%20by-goreleaser-green.svg)](https://github.com/goreleaser)
[![Go Doc](https://img.shields.io/badge/godoc-reference-blue.svg?style=flat-square)](http://godoc.org/github.com/llorllale/go-gitlint)
[![PDD status](http://www.0pdd.com/svg?name=llorllale/go-gitlint)](http://www.0pdd.com/p?name=llorllale/go-gitlint)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://raw.githubusercontent.com/llorllale/go-gitlint/master/LICENSE)

# go-gitlint
Lint your git!

## Usage
```
$ ./gitlint --help
usage: gitlint [<flags>]

Flags:
  --help                       Show context-sensitive help (also try --help-long and --help-man).
  --path="."                   Path to the git repo (default: ".").
  --subject-regex=".*"         Commit subject line must conform to this regular expression (default: ".*").
  --subject-maxlen=2147483646  Max length for commit subject line (default: math.MaxInt32 - 1).
  --subject-minlen=0           Min length for commit subject line (default: 0).
  --body-regex=".*"            Commit message body must conform to this regular expression (default: ".*").
  --body-maxlen=2147483646     Max length for commit body (default: math.MaxInt32 - 1)
  --since="1970-01-01"         A date in "yyyy-MM-dd" format starting from which commits will be analyzed (default: "1970-01-01").
  --msg-file=""                Only analyze the commit message found in this file (default: "").
  --max-parents=1              Max number of parents a commit can have in order to be analyzed (default: 1). Useful for excluding merge commits.
```
Additionally, it will look for configurations in a file `.gitlint` in the current directory if it exists. This file's format is just the same command line flags but each on a separate line. *Flags passed through the command line take precedence.*

### Lint your commit msg when committing

Add a `commit-msg` hook to your Git repo:

1. Create hook: `echo 'gitlint --msg-file=$1' > .git/hooks/commit-msg`
2. Make it executable: `chmod +x .git/hooks/commit-msg`

Now your commits will be validated after saving and closing the commit message in your text editor.

### Integrate to your CI

Use [`download-gitlint.sh`](https://raw.githubusercontent.com/llorllale/go-gitlint/master/download-gitlint.sh):

1. `curl https://raw.githubusercontent.com/llorllale/go-gitlint/master/download-gitlint.sh > download-gitlint.sh`
2. `chmod +x download-gitlint.sh`

Usage:
```
$ ./download-gitlint.sh -h
./download-gitlint.sh: download go binaries for llorllale/go-gitlint

Usage: ./download-gitlint.sh [-b] bindir [-d] [tag]
  -b sets bindir or installation directory, Defaults to ./bin
  -d turns on debug logging
   [tag] is a tag from
   https://github.com/llorllale/go-gitlint/releases
   If tag is missing, then the latest will be used.

 Generated by godownloader
  https://github.com/goreleaser/godownloader
```

### Exit codes

`gitlint`'s exit code will equal the number of issues found with your commit(s).

## Motivation

- [X] Validate format of commit message subject and body
- [X] Lint commit msgs on varios development platforms (Windows, Linux, Mac)
- [X] Configuration from file with cli args taking precedence
- [X] [`commit-msg`](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) hook to validate my commit's msg
- [X] Performance (because a slow pre-commit hook would render the git workflow unmanageable)
- [X] My first Go project :)

## Contributing
Fork this repo, make sure `make checks` works, **and then** open a PR.

## Build dependencies
To run `make checks` you will need:

* Go `1.11.x`
* Ruby 2.x (for `pdd`)
* [pdd](https://github.com/yegor256/pdd) (a ruby gem - `gem install pdd`)
* [golangci-lint](https://github.com/golangci/golangci-lint) v1.14.0 (expected to be in the `./bin` folder)
* [weasel](https://github.com/comcast/weasel) (`go get github.com/comcast/weasel`)

