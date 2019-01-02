## create-cloudflare-worker ![create-cloudflare-worker](https://img.shields.io/npm/v/create-cloudflare-worker.svg)

> A Starter Kit for Building a Cloudflare Worker

### Creating an App

To create a new worker with `create-cloudflare-worker`, run the following

```bash
npm init cloudflare-worker your-worker-name
```

or, with `npx`

```bash
npx create-cloudflare-worker your-worker-name
```

Once the installation is done, you can open your project folder:

```bash
cd my-app
```

### Building and testing your new worker

To build the worker, run

```bash
npm run build
```

This outputs the worker as `dist/main.js`.

To continually build the worker on every change, run

```bash
npm run watch
```

And finally, to execute the integration and unit tests, run

```bash
npm test
```

### Examples

We will add recipes here
- Building a API service with react-router
- Parsing Cookies

### Adding a Key Value Store

FIXME: How to add a KeyValue namespace

### Contributing
- Fork this Repo first
- Clone your Repo
- Install dependencies by `$ npm install`
- Checkout a feature branch
- Feel free to add your features
- Make sure your features are fully tested
- Publish your local branch, Open a pull request
- Enjoy hacking <3

### ISC

This work is licensed under the [ISC license](./LICENSE).

---
