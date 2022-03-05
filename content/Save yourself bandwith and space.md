---
slug: 5v3n-save-yourself-bandwith-and-space
---

# Save yourself bandwith and space

When I don't want to redownload all packages from a remote cache I'll use the `--no-substitute` switch.

Let me dissect the following command:

```shell
NIX_BUILD_SHELL=$(which bash) nix-shell shell.nix --no-substitute -I nixpkgs=file:///data/data/com.termux.nix/files/home/nixpkgs-3755a52ac8b2c5c69e67d495a0f4c5b88945a7f6.tar.gz
```

The `NIX_BUILD_SHELL=` prefix just avoids downloading bash itself from the cache.

The `nix-shell shell.nix` part is just an example, could also have used nix-build here.

`--no-substitute` then suppresses looking for files in one of the configured remote caches. While this is useful when I already fully built an expression and thus have all dependencies lying in a local store, it should not be used when the local store not yet contains all needed artifact i. e. prior first build.

Finally the `-I nixpkgs=` suffix might contain a path to a locally downloaded archive of one of the channels. In my case here the archive's name corresponds to the revision of the channel pinned in my sources.json as well.

There I should have all I needed when repeatedly building any kind of project be it haskell or julia just as an example and I wanted to save bandwidth as well as storage space on my device.

In another article I'll recall how I pushed all locally built artifacts belonging to a project to some remote cache of mine to also save build times on recurrent builds again using pinned revisions.
