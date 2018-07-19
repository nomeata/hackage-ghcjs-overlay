GHCJS package overlay for Hackage
=================================

It is possible to develop GHCJS applications with Cabal and `caba-install`,
just as if one were using GHC. Unfortunately, few people don't, and hence a
number of key packages are note being uploaded to Hackage. Until this is fixed,
this repository provides a cabal repository with these packages.

What is included?
-----------------

It includes:

 * `ghcjs-base`
 * `reflex`
 * `reflex-dom` and `reflex-dom-core`.


How do I use this?
------------------

Add this to your `~/.cabal/config`:

```
repository ghcjs-overlay
  url: http://hackage-ghcjs-overlay.nomeata.de/
  secure: True
  root-keys:
  key-threshold: 0
```

If you use new-style cabal commands, you can also add it to your
`cabal.project`, but you will have to use `cabal new-update` instead of `cabal
update`.

Can I use this on travis?
-------------------------

Yes you can! See <https://github.com/nomeata/ghcjs2gh-pages/> for an `.trais.yml`
file that builds your GHCJS program using this repo (and automatically deploys
your GHCJS program to Github Pages).

How is this created?
--------------------

Manually, so far: I pulled the github repositories, appended the current date
to the version, ran `cabal sdist` to get source tarballs, ran

```
$ hackage-repo-tool create-keys --keys keys
$ mkdir package/
$ mv .../**/*.tar.gz package/
$ hackage-repo-tool bootstrap --keys keys/ --repo .
```

and published this on Github Pages.

Some automation might be nice...

Do we really need this?
-----------------------

Only until these bugs are fixes:

* <https://github.com/ghcjs/ghcjs-base/issues/93>
* <https://github.com/reflex-frp/reflex/issues/177>
* <https://github.com/reflex-frp/reflex-dom/issues/140>

Concact
-------

This make-shift service is provided by Joachim Breitner <<mail@joachim-breitner.de>>.
It is hosted at <https://github.com/nomeata/hackage-ghcjs-overlay> where you can report issues.
