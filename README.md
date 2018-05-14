# vgo bug with versions

## Steps to reproduce

1. `go get github.com/OneOfOne/vgo-bug` (`go` *not* `vgo`).

2. `cd $GOROOT/src/go get github.com/OneOfOne/vgo-bug`.

3.

```
➤ vgo build
vgo: resolving import "github.com/alecthomas/kingpin"
vgo: finding github.com/alecthomas/kingpin (latest)
vgo: adding github.com/alecthomas/kingpin v1.3.7
vgo: resolving import "github.com/alecthomas/units"
vgo: finding github.com/alecthomas/units (latest)
vgo: adding github.com/alecthomas/units v0.0.0-20151022065526-2efee857e7cf

➤ cat go.mod
module github.com/OneOfOne/vgo-bug

require (
        github.com/alecthomas/kingpin v1.3.7 <<<
        github.com/alecthomas/units v0.0.0-20151022065526-2efee857e7cf
)
```

4. edit go.mod and change `v1.3.7` to `v2.2.6` (latest on github).

5.

```
➤ vgo build
vgo: resolving import "github.com/alecthomas/template"
vgo: finding github.com/alecthomas/template (latest)
vgo: adding github.com/alecthomas/template v0.0.0-20160405071501-a0175ee3bccc

➤ cat go.mod
module github.com/OneOfOne/vgo-bug

require (
        github.com/alecthomas/kingpin v0.0.0-20171217180838-947dcec5ba9c
        github.com/alecthomas/template v0.0.0-20160405071501-a0175ee3bccc
        github.com/alecthomas/units v0.0.0-20151022065526-2efee857e7cf
)

➤ vgo list -m
MODULE                          VERSION
github.com/OneOfOne/vgo-bug     -
github.com/alecthomas/kingpin   v0.0.0-20171217180838-947dcec5ba9c
github.com/alecthomas/template  v0.0.0-20160405071501-a0175ee3bccc
github.com/alecthomas/units     v0.0.0-20151022065526-2efee857e7cf
```
