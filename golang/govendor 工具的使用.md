## Go 的 Vendor 工具 -- govendor

```shell
go get -u github.com/kardianos/govendor
```

# 使用 Go modules

Go modules as a release and build tool are ready to use now. Tool support for Go modules (such as static analysis tools or auto-complete tools in editors) should be in a much better state when Go1.12 is released.

Please begin thinking about code organization in terms of modules today. Please begin to release modules with standardized build tags (vX.Y.Z) today. Please consider adding go.mod files to your projects if you consider them more of a "library" module. Please use Go modules in small or personal projects.

For larger code bases with many different programmers, you may wish to hold off on migrating to Go modules until you have verified that all your existing tooling (editors, static analizers, and code generators) have support for Go modules.

# Govendor 介绍

New users please read the [FAQ](https://github.com/kardianos/govendor/blob/master/doc/faq.md)

Package developers should read the [developer guide](https://github.com/kardianos/govendor/blob/master/doc/dev-guide.md).

For a high level overview read the [whitepaper](https://github.com/kardianos/govendor/blob/master/doc/whitepaper.md)

Uses the go1.5+ vendor folder. Multiple workflows supported, single tool.

[![Build Status](https://camo.githubusercontent.com/e327942e625c3830ecad416269a8e88dcc0026a2/68747470733a2f2f7472617669732d63692e6f72672f6b61726469616e6f732f676f76656e646f722e7376673f6272616e63683d6d6173746572)](https://travis-ci.org/kardianos/govendor) [![Build status](https://camo.githubusercontent.com/fa28695bf2db9c8d9b7e2d98b2d9ded032963a3b/68747470733a2f2f63692e6170707665796f722e636f6d2f6170692f70726f6a656374732f7374617475732f736b66317433333633793674796375632f6272616e63682f6d61737465723f7376673d74727565)](https://ci.appveyor.com/project/kardianos/govendor/branch/master) [![GoDoc](https://camo.githubusercontent.com/f975d2a7939add6bca926dae994eff68ee912b19/68747470733a2f2f676f646f632e6f72672f6769746875622e636f6d2f6b61726469616e6f732f676f76656e646f723f7374617475732e737667)](https://godoc.org/github.com/kardianos/govendor)

- Copy existing dependencies from $GOPATH with `govendor add/update`.
- If you ignore `vendor/*/`, restore dependencies with `govendor sync`.
- Pull in new dependencies or update existing dependencies directly from remotes with `govendor fetch`.
- Migrate from legacy systems with `govendor migrate`.
- Supports Linux, OS X, Windows, probably all others.
- Supports git, hg, svn, bzr (must be installed and on the PATH).

## 注意事项

- 工程必须在 $GOPATH/src 目录下
- 如果使用 go1.5版本, ensure you `set GO15VENDOREXPERIMENT=1`.

### 快速开始，也可以查看 [FAQ](https://github.com/kardianos/govendor/blob/master/doc/faq.md)

```shell
# 创建工程
cd "my project in GOPATH"
govendor init

# 将 GOPATH 中已存在的文件添加进 vendor 目录中
govendor add +external

# View your work.
govendor list

# Look at what is using a package
govendor list -v fmt

# Specify a specific version or revision to fetch
govendor fetch golang.org/x/net/context@a4bbce9fcae005b22ae5443f6af064d80a6f5a55
govendor fetch golang.org/x/net/context@v1   # Get latest v1.*.* tag or branch.
govendor fetch golang.org/x/net/context@=v1  # Get the tag or branch named "v1".

# Update a package to latest, given any prior version constraint
govendor fetch golang.org/x/net/context

# Format your repository only
govendor fmt +local

# Build everything in your repository only
govendor install +local

# Test your repository only
govendor test +local
```

## 子命令

```
init     Create the "vendor" folder and the "vendor.json" file.
list     List and filter existing dependencies and packages.
add      Add packages from $GOPATH.
update   Update packages from $GOPATH.
remove   Remove packages from the vendor folder.
status   Lists any packages missing, out-of-date, or modified locally.
fetch    Add new or update vendor folder packages from remote repository.
sync     Pull packages into vendor folder from remote repository with revisions from vendor.json file.
migrate  Move packages from a legacy tool to the vendor folder with metadata.
get      Like "go get" but copies dependencies into a "vendor" folder.
license  List discovered licenses for the given status or import paths.
shell    Run a "shell" to make multiple sub-commands more efficient for largeprojects.

go tool commands that are wrapped:
`+<status>` package selection may be used with them fmt, build, install, clean, test, vet, generate, tool
```

## 状态

Packages can be specified by their "status".

```
	+local    (l) packages in your project
	+external (e) referenced packages in GOPATH but not in current project
	+vendor   (v) packages in the vendor folder
	+std      (s) packages in the standard library

	+excluded (x) external packages explicitly excluded from vendoring
	+unused   (u) packages in the vendor folder, but unused
	+missing  (m) referenced packages but not found

	+program  (p) package is a main package

	+outside  +external +missing
	+all      +all packages
```

Status can be referenced by their initial letters.

- `+std` same as `+s`
- `+external` same as `+ext` same as `+e`
- `+excluded` same as `+exc` same as `+x`

Status can be logically composed:

- `+local,program` (local AND program) local packages that are also programs
- `+local +vendor` (local OR vendor) local packages or vendor packages
- `+vendor,program +std` ((vendor AND program) OR std) vendor packages that are also programs or std library packages
- `+vendor,^program` (vendor AND NOT program) vendor package that are not "main" packages.

## 包限定符

The full package-spec is: `<path>[{/...|/^}][::<origin>][@[<version-spec>]]`

Some examples:

- `github.com/kardianos/govendor` specifies a single package and single folder.
- `github.com/kardianos/govendor/...` specifies `govendor` and all referenced packages under that path.
- `github.com/kardianos/govendor/^` specifies the `govendor` folder and all sub-folders. Useful for resources or if you don't want a partial repository.
- `github.com/kardianos/govendor/^::github.com/myself/govendor` same as above but fetch from user "myself".
- `github.com/kardianos/govendor/...@abc12032` all referenced packages at revision `abc12032`.
- `github.com/kardianos/govendor/...@v1` same as above, but get the most recent "v1" tag, such as "v1.4.3".
- `github.com/kardianos/govendor/...@=v1` get the exact version "v1".

## 包和状态

You may specify multiple package-specs and multiple status in a single command. Commands that accept status and package-spec:

- list
- add
- update
- remove
- fetch

You may pass arguments to govendor through stdin if the last argument is a "-". For example `echo +vendor | govendor list -` will list all vendor packages.

## 忽略构建标签和排除包

Ignoring build tags is opt-out and is designed to be the opposite of the build file directives which are opt-in when specified. Typically a developer will want to support cross platform builds, but selectively opt out of tags, tests, and architectures as desired.

To ignore additional tags edit the "vendor.json" file and add tag to the vendor "ignore" file field. The field uses spaces to separate tags to ignore. For example the following will ignore both test and appengine files.

```
{
	"ignore": "test appengine",
}
```

Similarly, some specific packages can be excluded from the vendoring process. These packages will be listed as `excluded`(`x`), and will not be copied to the "vendor" folder when running `govendor add|fetch|update`.

Any sub-package `foo/bar` of an excluded package `foo` is also excluded (but package `bar/foo` is not). The import dependencies of excluded packages are not listed, and thus not vendored.

To exclude packages, also use the "ignore" field of the "vendor.json" file. Packages are identified by their name, they should contain a "/" character (possibly at the end):

```
{
	"ignore": "test appengine foo/",
}
```