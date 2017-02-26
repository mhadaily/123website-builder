#123website builder

an experimental static website builder based on Silex and Powered by Nodejs. [live demo](https://mj123website.herokuapp.com/)

##Installation on your local computer

This is for developers only, since our beloved designers can use the [online version](https://mj123website.herokuapp.com/).

### Recommended: with Docker

Prerequisite :
* [docker](https://www.docker.com/)

```
$ docker-compose up
```

Open http://localhost:6805/ and you are ready!

### local installation on linux or macos or cloud9

Prerequisite:

* [node.js](http://nodejs.org/) installed
* [NPM](https://npmjs.org/) installed
* [python](https://www.python.org/downloads/) (version >= V2.7)
* [java](https://www.java.com/en/download/index.jsp) (version >= 7)

Clone this repository, and do not forget the sub modules (cloud-explorer and unifile)

```
$ git clone --recursive https://github.com/mhadaily/123website-builder.git
```

Install all needed modules and build the assets

```
$ npm install
$ npm run build
```

Start the server and then open [http://localhost:6805/](http://localhost:6805/) - note that the port is 6805, which is easy to remember, since it is the date of sexual revolution started in paris france 8-)

```
$ npm start
```

And finally, take a look at the "available commands" section bellow

### Available commands

If you develop or debug Silex, these npm scripts can be used with npm (they are defined in the file [package.json](./package.json))

* `$ npm start` will start the server
* `$ npm run start:debug` will start the server in debug mode (no error catchall, enable local service to use local file system as a storage)
* `$ npm run build` will build the client side code (html, css, js), ready for production
* `$ npm run build:server` this only check that the server scripts are correct
* `$ npm run watch:client` will watch the html, js and css source folders and rebuild when a file changes

### environment variables

* `PORT`, optional, default: 6805, [used here in the code](dist/server/server.js#L148)
* `SSL_PORT`, optional, default: to 443, [used here in the code]()
* `SILEX_FORCE_HTTPS`, optional [used here in the code](dist/server/server.js#102) to force https/ssl (default is `false`)
* `SILEX_SSL_PRIVATE_KEY`, optional (see ssl section bellow), [used here in the code](dist/server/server.js#L124)
* `SILEX_SSL_CERTIFICATE`, optional (see ssl section bellow), [used here in the code](dist/server/server.js#L124)
* `SILEX_SESSION_FOLDER`, optional, default: `dist/sessions`, [used here in the code](dist/server/server.js#L53)
* `SILEX_DEBUG`, optional, default: `false`, when `true` this will enable the service "www" (storage on the local server in `www/`) with login `admin` and pass `admin`, [used here in the code](dist/server/server.js#L78)
* `RESTART_ROUTE`, optional, if set it will enable the route `GET {{Silex server instance URL}}/tasks/{{RESTART_ROUTE}}` which will restart the server, [used here in the code](dist/server/silex-tasks.js#L58). See [this article to learn about deployment and why this hack](http://the.webapp.cat/2015/07/Deploy-to-Gandi-Simple-Hosting.html).
* `GITHUB_CLIENT_ID` and `GITHUB_CLIENT_SECRET`: optional, to activate github service, you need to create a github app to get these info ([create a github app](https://github.com/settings/applications/new) to get those)

### enable https / SSL

When you start Silex, it looks for the environment variables `SILEX_SSL_PRIVATE_KEY` and `SILEX_SSL_CERTIFICATE`. If they are present, it enables SSL.

`SILEX_SSL_PRIVATE_KEY` is expected to be the path to a `.key` file, and `SILEX_SSL_CERTIFICATE` the path to a  `.crt`.
