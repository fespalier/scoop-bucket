# fespalier Scoop bucket

The Scoop manifest for [`fsp`](https://github.com/fespalier/fespalier), the generator behind
fespalier's file-tree routing for Flutter. One manifest, `fsp`, for 64-bit Windows (x86_64).

## Install

```powershell
scoop bucket add fespalier https://github.com/fespalier/scoop-bucket
scoop install fespalier/fsp
```

Check it:

```powershell
fsp --version
```

## Upgrade and uninstall

```powershell
scoop update
scoop update fsp
scoop uninstall fsp
scoop bucket rm fespalier
```

The manifest always names the latest fespalier release. To pin an older one, use the install script
with `$env:FSP_VERSION` (below), or `dart run fespalier`, which runs the `fsp` that matches the
package version in your `pubspec.yaml`.

## Troubleshooting

**`scoop update fsp` says it is already up to date, but a newer release is out.** Run `scoop update`
first: the bucket is a git clone, and only `scoop update` pulls the new manifest.

**The bucket was added before its first manifest, or its clone is broken** (`scoop install` cannot
find `fsp`). Remove the bucket and add it again:

```powershell
scoop bucket rm fespalier
scoop bucket add fespalier https://github.com/fespalier/scoop-bucket
scoop install fespalier/fsp
```

**Without the bucket.** Every fespalier release also attaches its own `fsp.json`, naming that
release's archive and SHA-256:

```powershell
scoop install https://github.com/fespalier/fespalier/releases/latest/download/fsp.json
```

A manifest installed from a URL does not update from the bucket: to move to a newer release,
`scoop uninstall fsp` and run that command again.

## Without Scoop

```powershell
irm https://raw.githubusercontent.com/fespalier/fespalier/main/install.ps1 | iex
```

The script puts `fsp.exe` in `%LOCALAPPDATA%\fespalier\bin` (change it with `$env:FSP_INSTALL_DIR`,
pick a release with `$env:FSP_VERSION`), checks the SHA-256, and prints how to add that folder to
your `PATH`. The other install routes are in fespalier's
[getting started](https://github.com/fespalier/fespalier/blob/main/docs/getting-started.md).

## How this bucket is updated

`bucket/fsp.json` is written by fespalier's release workflow on every release, from archives it has
verified against the checksums pinned in that release. Don't edit it by hand: the next release
overwrites it. Report problems in
[fespalier/fespalier](https://github.com/fespalier/fespalier/issues).
