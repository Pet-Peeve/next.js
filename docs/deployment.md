---
description: Compile and deploy your Next.js app to production with ZEIT Now and other hosting alternatives.
---

# Deployment

To go to production Next.js has a `next build` command. When run, it will compile your project and automatically apply numerous optimizations.

## Prepare your package.json

Ensure your `package.json` has the `"build"` and `"start"` scripts:

```json
{
  "scripts": {
    "dev": "next",
    "build": "next build",
    "start": "next start"
  }
}
```

In the case that you'd want to do a [full static export](/docs/advanced-features/static-html-export.md) of the Next.js application add `next export` to the `"build"` script:

```json
{
  "scripts": {
    "dev": "next",
    "build": "next build && next export",
    "start": "next start"
  }
}
```

## ZEIT Now

The easiest way to deploy Next.js to production is using the [ZEIT Now platform](https://zeit.co) from the creators of Next.js.

### Preview deployments

ZEIT Now integrates directly with GitHub, GitLab, and Bitbucket to give you a unique shareable url for every commit and every pull request. This url can be shared with customers and can be used to run integration tests against.

### Hybrid Next.js

The [hybrid pages](/docs/basic-features/pages.md) approach is fully supported out of the box. Meaning that every page can either use [Static Generation](/docs/basic-features/pages.md#static-generation) or [Server-Side Rendering](/docs/basic-features/pages.md#server-side-rendering).

In case of [Static Generation](/docs/basic-features/pages.md#static-generation) the page will automatically be served from the ZEIT Now Smart CDN.

When the page is using [Server-Side Rendering](/docs/basic-features/pages.md#server-side-rendering) it will become an isolated serverless function automatically. This allows the page rendering to scale automatically and be independent—errors on one page won't affect another.

API routes will also become separate serverless functions that execute and scale separately from each other.

### CDN + HTTPS by default

Assets (JavaScript, CSS, images, fonts etc) and Statically Generated pages are automatically served through the ZEIT Now Smart CDN, ensuring these are always served close to your users.

HTTPS is enabled by default and doesn't require extra configuration.

### Getting started

#### From a git repository

You can link your project in [GitHub](https://zeit.co/new), [GitLab](https://zeit.co/new), or [Bitbucket](https://zeit.co/new) through the [web interface](https://zeit.co/new). This will automatically set up deployment previews for pull requests and commits.

#### Through the ZEIT Now CLI

You can install the command line tool using npm:

```
npm install -g now
```

You can deploy your application by running the following command in the root of the project directory:

```
now
```

You will receive a unique link similar to the following: https://your-project.username.now.sh.

## Self hosting

Next.js can be deployed to any hosting provider that supports Node.js. In order to self-host there are two commands: `next build` and `next start`.

`next build` builds the production application in the `.next` folder.

`next start` starts a Node.js server that supports [hybrid pages](/docs/basic-features/pages.md), serving both statically generated and server-side rendered pages.

Generally you'll have to follow these steps to deploy to production:

- Run `npm install`
- Run `npm run build` (runs `next build`)
- Potentially copy the `.next`, `node_modules`, and `package.json` to your server.
- Run `npm run start` (runs `next start`) on the server

In case you're doing a full static export using `next export` the steps are slightly different and don't involve using `next start`:

- Run `npm install`
- Run `npm run build` (runs `next build && next export`)
- A `out` directory is generated by `next export`
- Copy the `out` directory to the server and make sure it's served by your server