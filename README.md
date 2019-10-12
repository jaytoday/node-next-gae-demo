# node-next-gae-demo
A simple working example of running [Next.js](https://nextjs.org/) on Google App Engine's [Node Standard Environment](https://cloud.google.com/appengine/docs/standard/nodejs/)

**Update**:
* v0.2.1 - 2019-10-12
  * Upgraded several packages
* v0.2.0 - 2019-07-21
  * Upgraded to [Next.js 9](https://nextjs.org/blog/next-9)
  * Switched routing to Next.js 9's [filebased routing](https://github.com/zeit/next.js#dynamic-routing) and removed routes from server.js
  * Retooled `start` script for better deployed ngnix performance
  * Introduced `start-local` for separating local run from deployed runs
  * Upgraded various packages

* v0.1.1 - 2019-07-16:
  * Upgraded axios, js-yaml, and lodash packages for security

* v0.1.1 - 2019-03-30:
  * Upgraded eslint to avoid js-yaml security vulnerability
  * Removed isopmorphic-unfetch in lieu of axios
  * Added gzip compression
  * Minor prep for PWA

* v0.1.0 - 2019-03-09:
  * Upgraded to Next.js 8.0.3
  * Upgraded react and react dom to 16.8.3 (aka "the one with hooks")
  * Various other package updates

* v0.0.4 - 2018-12-29:
  * Updated to use nodejs10 runtime on App Engine
  * Upgraded to Next.js 7.0.2

# Live Demo
**View live demo at [http://node-next-gae-demo.blaine-garrett.appspot.com/](http://node-next-gae-demo.blaine-garrett.appspot.com/)**

* Be sure to also check out this demo [with material-ui support](https://github.com/blainegarrett/material-node-next-gae-demo).


# Development
Note: You need [node](https://nodejs.org) installed. I am using v8.11.3

**Installation:** `npm install`

**Local Development:**: `npm run dev` Point browser to localhost:3000

**Production Build:** `npm run build` (Note: It is a good idea to remove your ./build dir before build/deploy to remove unused build files)

**Running Production Build Locally:** `npm run start-local` Point browser to localhost:8080


# Deploying to Google App Engine
This will deploy your build to a version of the `node-next-gae-demo` service (as defined in app.yaml) in your *<your_project_id>* project. Learn more about [services](https://cloud.google.com/appengine/docs/standard/python/microservices-on-app-engine) and [versions](https://cloud.google.com/appengine/docs/admin-api/deploying-apps) in GAE).

`gcloud --project your_project_id app deploy app.yaml --version version_name --verbosity=debug`

eg: `gcloud --project blaine-garrett app deploy app.yaml --version main --verbosity=debug`


**Prerequisites**:
* You must have a Google Cloud Account created. [Sign up here](https://cloud.google.com/).
* You must have a project created. Replace *your_project_id* with the id of your project.
* You must have the Google Cloud SDK command line tools installed. [Installation Instructions](https://cloud.google.com/sdk/)

# Important Notes for GAE
* Unlike other runtimes supported by App Engine (Python 2.7, etc), you cannot run your application locally via dev_appserver.py or equivalent. You must use the node runtime installed to your machine.
* As of Dec 29th, 2018 not all Google Cloud and App Engine standard features are available yet in the Beta.

# Important Notes for Next.js
* As of March 13th, 2018, files and folders are automatically skipped during deploy if they start with a `.`. This means the default .build directory must be renamed using the `distDir` setting in ./next.config


# About the Demo
This demo is a compilation of the [nextgram](https://github.com/now-examples/nextgram), [custom-server-express](https://github.com/zeit/next.js/tree/master/examples/custom-server-express) and [head-elements](https://github.com/zeit/next.js/tree/master/examples/head-elements) examples from Next.js

It pulls data from the Minneapolis Institute of Art's [Elastic Search api](https://github.com/artsmia/collection-elasticsearch).

It demonstrates resolving data dependencies server side (and client side), setting meta content, as well as returning 404 status codes server side based on the results of the REST data.

The demo was presented as part of a lightning talk about Node/Next/GAE at the [React Minneapolis Meetup](https://www.meetup.com/React-Minneapolis-Meetup/) March 15th, 2018 with permission from the GAE Node.js team while Node support was still in EAP. [View slides for the presentation](https://docs.google.com/presentation/d/1pUc8VbT4J5ca4qe2zIbqezO6EhLER6E_e5WgsGitDr0/edit?usp=sharing).
