# Use pixi on Uppcoder

Every [Uppcoder](https://uppcoder.com) app comes with [pixi](https://pixi.sh), the package manager from [prefix.dev](https://prefix.dev), and its own `pixi.toml`. This guide shows how to add libraries and tools, run tasks and bring your own pixi project, from the terminal in your browser.

Every step below was tested on Uppcoder on 20 November 2026 (pixi 0.62.2). The same guide is on our site: **[portal.uppcoder.com/guides/use-pixi](https://portal.uppcoder.com/guides/use-pixi)**. Corrections are welcome as issues or pull requests.

## Contents

- [What you already have](#what-you-already-have)
- [Add a library to your app](#add-a-library-to-your-app)
- [Install a tool, no root needed](#install-a-tool-no-root-needed)
- [Save commands as tasks](#save-commands-as-tasks)
- [Bring your own pixi project](#bring-your-own-pixi-project)
- [Good to know](#good-to-know)

## What you already have

Open your app and its terminal (or connect over SSH). In the app folder you will find:

- `pixi.toml`: your app's manifest. It is yours to read, change and commit.
- `pixi.lock`: the exact versions, so the same environment comes back every time.
- Packages come from conda-forge, where most Python and Node libraries and many command-line tools live.
- The welcome text in the terminal shows the name of your app's environment, for example `web-fastapi`.

## Add a library to your app

In the app folder:

```bash
pixi add httpx
```

It is written into `pixi.toml` and `pixi.lock` and is ready straight away: `python` in the terminal can import it, and so can your app. Frameworks that run in reload mode pick it up on your next save; if yours does not, press **Restart** on the stack page.

To take a library out again:

```bash
pixi remove httpx
```

## Install a tool, no root needed

Command-line tools go in with `add`:

```bash
add htop
```

It installs into your app's own environment, so you do not need `sudo`, and the tool is there in every new terminal. `remove htop` takes it out.

## Save commands as tasks

Commands you run often can be saved in `pixi.toml` as tasks:

```bash
pixi task add seed "python seed.py"
pixi run seed
pixi task list
```

If a task needs your app's libraries, run it in your app's environment (use the name the terminal shows):

```bash
pixi run -e web-fastapi seed
```

Leave the `init` and `start` tasks that came with your app as they are: Uppcoder uses them to start the app.

## Bring your own pixi project

A project that already has a `pixi.toml` works as it does on your laptop. Clone it into a folder of its own, not into the app folder itself (that one has its own `pixi.toml`):

```bash
git clone <your repository> ~/projects/myproject
cd ~/projects/myproject
pixi install
pixi run start
```

## Good to know

- Commit `pixi.toml` and `pixi.lock` with your code, so the environment travels with it.
- pixi itself is installed and kept up to date by Uppcoder.
- This guide covers libraries from conda-forge; check a package exists there first ([prefix.dev](https://prefix.dev/channels/conda-forge) or [anaconda.org](https://anaconda.org/conda-forge)).
- The free plan runs one app with one database; your own pixi projects in folders run inside that app.

## Try it

Sign up at [portal.uppcoder.com](https://portal.uppcoder.com): the free plan needs no card and has no time limit. This guide on our site: [portal.uppcoder.com/guides/use-pixi](https://portal.uppcoder.com/guides/use-pixi). More guides: [portal.uppcoder.com/guides](https://portal.uppcoder.com/guides). How we built Uppcoder on pixi: [websson-doo.com blog](https://websson-doo.com/en/blog/how-we-built-uppcoder-on-pixi/).

---

pixi is an open-source project by [prefix.dev](https://prefix.dev). This guide is by [Websson](https://websson-doo.com), the company behind Uppcoder, and is licensed [CC BY 4.0](LICENSE).
