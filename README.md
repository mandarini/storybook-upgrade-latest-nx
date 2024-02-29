# Nx 18 + Storybook 8

## If you want to repro the issue

1. Clone this repo
2. Run `npm install`
3. Run `nx storybook rapp1`

### How I created this repo

This is how I created this repo, no need to do these steps too, since I already did them.

1. I generated a new Nx workspace using `npx create-nx-workspace@latest` using React as preset
2. I added Storybook using `nx g @nrwl/react:storybook-configuration`
3. I ran `npx storybook@next upgrade --config-dir apps/rapp1/.storybook` to upgrade Storybook to `next` version

## Issue

Storybook runs successfully, however I got this warning:

```bash
nx storybook rapp1

> nx run rapp1:storybook

@storybook/cli v8.0.0-rc.0

Storybook failed to check addon compatibility Error: No Storybook dependencies found in the package.json
    at getIncompatibleStorybookPackages (/Users/fileas/Projects/nrwl/test-nx-workspaces/story-latest/node_modules/@storybook/core-server/dist/index.js:53:358)
    at async warnOnIncompatibleAddons (/Users/fileas/Projects/nrwl/test-nx-workspaces/story-latest/node_modules/@storybook/core-server/dist/index.js:56:95)
    at async buildDevStandalone (/Users/fileas/Projects/nrwl/test-nx-workspaces/story-latest/node_modules/@storybook/core-server/dist/index.js:65:1807)
    at async withTelemetry (/Users/fileas/Projects/nrwl/test-nx-workspaces/story-latest/node_modules/@storybook/core-server/dist/index.js:28:3579)
    at async dev (/Users/fileas/Projects/nrwl/test-nx-workspaces/story-latest/node_modules/@storybook/cli/dist/generate.js:634:563)
    at async Command.<anonymous> (/Users/fileas/Projects/nrwl/test-nx-workspaces/story-latest/node_modules/@storybook/cli/dist/generate.js:636:250)
info => Starting manager..
info => Starting preview..
The CJS build of Vite's Node API is deprecated. See https://vitejs.dev/guide/troubleshooting.html#vite-cjs-node-api-deprecated for more details.
╭──────────────────────────────────────────────────────╮
│                                                      │
│   Storybook 8.0.0-rc.0 for react-vite started        │
│   82 ms for manager and 619 ms for preview           │
│                                                      │
│    Local:            http://localhost:52150/         │
│    On your network:  http://192.168.68.115:52150/    │
│                                                      │
╰──────────────────────────────────────────────────────╯
^C%
```

1. The `npx storybook upgrade` command created a `package.json` in my `apps/rapp1` project directory.
2. Storybook does not take into account the root `package.json` and looks inside the project-level `package.json` only to check for Storybook dependencies.

## Other notes

Everything else works as expected!

### All Storybook commands work

```bash
nx build-storybook rapp1
```

```bash
nx storybook rapp1
```

and while `storybook` is running then run:

```bash
nx test-storybook rapp1 --url  http://localhost:52062/ (or whichever port it is running on)
```

```bash
nx static-storybook rapp1
```
