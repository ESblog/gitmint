# Gitmint


A mint on Gitment, the gitment is a comment system based on GitHub Issues.

[Demo Page](https://imsun.github.io/gitment/)

[中文简介](https://imsun.net/posts/gitment-introduction/)

[新增特性](https://aimingoo.github.io/1-1725.html)

- [Features](#features)
- [Get started](#get-started)
- [New Features](#new-features)
- [Methods and Customize](#methods-and-customize)
- [About Security](#about-security)
- [History](#history)

## Features

- [Gitment based](https://github.com/imsun/gitment)
- No server-side implementation
  - to choose both https://gh-oauth.imsun.net and [gh-oauth-server](https://github.com/imsun/gh-oauth-server), or
  - php oauth proxy [intersect](https://github.com/aimingoo/intersect), or
  - other api proxy/gateway
- Force redirect protocol to support HTTPS/HTTP Github pages site, 
- Support urlencoded for GET request and response data
- Language translator for default/other theme, a simple method
- No client_secret

## Get Started

### 1. Install

```html
<link rel="stylesheet" href="https://aimingoo.github.io/gitmint/style/default.css">
```

```html
<script src="https://aimingoo.github.io/gitmint/dist/gitmint.browser.js"></script>
```

or via npm and build it:

```sh
> git clone https://github.com/aimingoo/gitmint
> cd gitmint
> npm install && npm run build

# dist files
> ls style/default.css
> ls dist/gitmint.browser.js
```

or via npm module only:

```sh
> npm install --save gitmint
## and in js:
## import Gitmint from 'gitmint'
```

### 2. Register An OAuth Application

[Click here](https://github.com/settings/applications/new) to register an OAuth application, and you will get a client ID and a client secret.

Make sure the callback URL is right. Generally it's the origin of your site, like `https://YOURNAME.github.io`, or `https://your-site`.

### 3. Create and render a gitment

```javascript
const gitment = new Gitmint({
  id: 'Your page ID', // optional
  owner: 'Your GitHub ID',
  repo: 'The repo to store comments',
  oauth: {
    client_id: 'Your client ID',
    client_secret: 'Your client secret',
    // proxy_gateway: 'Your proxy service, either this or client_secret'
  },
  // ...
  // For more available options, check out the documentation below
})

gitment.render('comments')
// or
// gitment.render(document.getElementById('comments'))
// or
// document.body.appendChild(gitment.render())
```

### 4. Initialize Your Comments

maybe, you need a automation tool.

## New features

### proxy_gateway support

no `client_secret` when create gitment instance, either proxy_gateway or client_secret. ex:

```javascript
const gitment = new Gitmint({
  ...
  oauth: {
    client_id: 'Your client ID',
    proxy_gateway: 'https://YOUR_PROXY'
  },
  ...
```

proxy/gateway is a service, @see [aimingoo/intersect](https://github.com/aimingoo/intersect)

### Language translator

translator module is included, use it in your theme. example in src/theme/default.js:

```javascript
import { chinese as $ } from '../translator'
...

// translate 'Comment' from english to chinese
submitButton.innerText = $('Comment')
```

update the translator.js module to support more text and languages.

### Force redirect protocol

update const `force_redirect_protocol` in gitment.js, make sure it same to protocol of the callback URL in Github OAuth application's settings.

## Methods and Customize

@see [https://github.com/imsun/gitment#methods](https://github.com/imsun/gitment#methods)


## About Security

@see [https://github.com/imsun/gitment#about-security](https://github.com/imsun/gitment#about-security), and [https://github.com/imsun/gitment/pull/25#issuecomment-314352684](https://github.com/imsun/gitment/pull/25#issuecomment-314352684)

## History

```
2017.07.12 create gitmint, first release.
2017.05.30 fork and push some commits to Gitment.
```