# x86recomp.github.io

The site for [x86recomp](https://github.com/JTM-rootstorm/x86recomp) and
the game ports built on it, by system, served by GitHub Pages (Jekyll,
no Actions).

- `index.md`: the landing page; its systems and port list are generated.
- `_systems/<system>.md`: one page per system (PC, PS4, Switch, Xbox 360). `order`
  sets its position in the Systems menu.
- `_projects/<system>/<port>.md`: one page per port, served at
  `/<system>/<port>/`. The front matter holds the status shown on the
  landing page (`stage` is one of `playable`, `ingame`, `boots`, `early`
  and sets the badge colour; `order` the position in its system); the
  body is the status write-up. A new system's folder also needs a
  `system:` default in `_config.yml`.
- `theme` and `fonts` (a Google Fonts `css2` query) give a port's page
  its own look; the themes are in `assets/themes.css`.

Preview locally:

```sh
jekyll serve
```
