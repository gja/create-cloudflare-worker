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

### Running the worker locally

To run the worker locally, run

```bash
npm start
```

This will start the worker on port 4000, and forward all requests to the upstream server at `http://localhost:3000`. This will allow you to develop your application in tandem with the worker that will front the application.

### Deploying

This project may be used to deploy your newly built worker to cloudflare as follows:

```bash
CF_ACCOUNT=acct-id CF_WORKER_NAME=worker-name CF_EMAIL=you@you.com CF_AUTH_KEY=auth-key npm run deploy
```

However, you may also just copy dist/main.js and paste it into the CF worker dashboard (or even terraform it)

### Examples

We will add recipes here
- Building a API service with react-router
- Parsing Cookies

### Adding a Key Value Store

This project can also mock an in memory KV Store. This can be done as follows

- Add the kv store (ex: MYSTORE) to the list of global variables of the worker
- When running the worker, start the worker with the `KV_NAMESPACES` as follows `KV_NAMESPACES=MYSTORE,OTHER_STORE npm start`
- In tests, namespaces can be created as an option to createTestApp as follows: `const app = createTestApp(workerContents, upstreamApp, { kvStores: ["MYSTORE"] })`. The new store can be accessed in tests as follows: `await app.stores.MYSTORE.put("key", "value")`. `await app.stores.MYSTORE.get("key")`

When you are ready to deploy your new worker with a KV:

- run curl to create the worker namespace (this should only be done once)
```bash
# If this fails, contact support
curl "https://api.cloudflare.com/client/v4/accounts/$CF_ACCOUNT/workers/namespaces" \
  -X POST \
  -H "X-Auth-Email: $CF_EMAIL" \
  -H "X-Auth-Key: $AUTH_KEY" \
  -H "Content-Type: application/json" \
  --data '{"title": "your-namespace"}'
# {"result":{"id": "<some-id>","title":"your-namespace"}}
```
- Bind this namespace in the deploy script in package.json. Find the bindings section in the deploy script, and replace it with something like this
```
\\\"bindings\\\":[{\\\"name\\\":\\\"MYSTORE\\\",\\\"type\\\":\\\"kv_namespace\\\",\\\"namespace_id\\\":\\\"$MYSTORE_ID\\\"}]
```
- Finally, run your deploy script with the MYSTORE_ID variable set to the id returned by the curl command.

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
