# Test MFE

This repository is a small **test micro-frontend remote** built with **React**, **TypeScript**, **Vite**, and **module federation**.

Its main purpose is to provide a lightweight remote app that can be:

- developed standalone during local work
- exposed to a host shell as a federated module
- used for experimenting with layout, data display, and micro-frontend integration

The current app is a Palmer Penguins explorer with:

- an **Explorer** view containing a scatterplot and controls
- a **Dataset** view containing source information and metadata about the JSON dataset

## What this repo exposes

The remote is exposed through Vite federation as:

- `./HRApp` -> `./src/App.tsx`

The federation build produces `remoteEntry.js`, which a host shell can consume.

## Tech stack

- React 19
- TypeScript
- Vite
- `@originjs/vite-plugin-federation`
- ESLint

## Installation

This repo uses **Yarn**.

```bash
yarn install
```

## Local development

Run the app locally with:

```bash
yarn dev
```

Vite serves the app on:

- `http://localhost:5176`

`src/main.tsx` bootstraps the same `App` component for standalone development, while `src/App.tsx` is also the federated remote entry.

## Build

Create a production build with:

```bash
yarn build
```

Build output is written to:

- `dist/`

## Preview the built app

To preview the normal Vite build:

```bash
yarn preview
```

To build first and serve the federated output on the expected port:

```bash
yarn serve:federated
```

That command is useful when you want a host shell to load the built remote from a stable local URL.

## Linting

Run ESLint with:

```bash
yarn lint
```

## Tests

There is currently **no test runner configured** in this repository.

At the moment, the supported validation commands are:

```bash
yarn build
yarn lint
```

## Project structure

```text
src/
  App.tsx                    # app shell and view switching
  components/
    DatasetView.tsx          # dataset information view
    ExplorerView.tsx         # scatterplot explorer view
  data/
    penguins.json            # Palmer Penguins source data
  penguins.ts                # normalization, constants, and shared helpers
  main.tsx                   # standalone development bootstrap
```

## Micro-frontend notes

- The app is a **remote**, not a full host shell.
- `vite.config.ts` sets the federation name to `test-mfe`.
- `react` and `react-dom` are shared as singletons.
- The Vite base path is set to `/test-mfe/`, which is important for GitHub Pages-style deployment.
- Both dev and preview are pinned to port `5176`.



