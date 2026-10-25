# x86recomp.github.io

The site for [x86recomp](https://github.com/JTM-rootstorm/x86recomp) and
the game ports built on it, served by GitHub Pages (Jekyll, no Actions).

- `index.md`: the landing page; its project list is generated.
- `_projects/<name>.md`: one page per port. The front matter holds the
  status shown on the landing page (`stage` is one of `playable`,
  `ingame`, `boots`, `early` and sets the badge colour; `order` the
  position); the body is the status write-up.

Preview locally:

```sh
jekyll serve
```
