# Custom React App
_Any commands below will assume you're using `yarn`. If you're not, you can install it [here](https://yarnpkg.com/en/docs/install). If you're still not, replace `yarn` with `npm install`, and `yarn start|test|build` with `npm start|test|build`, and just swap `yarn` for `npm` in any other commands._

`create-react-app` is a great way to bootstrap a new site, and comes with a number of other benefits: config is hidden away in one dependency, leaving you to get on with the important stuff and taking a load off your mind; you can update a project with the latest of all this config and tooling in-place, in a few seconds; and every project built with it has a familiar base reducing the ramp-up time as you and your teammates switch projects.

### The Problem
All of this is great, but sometimes you need that extra bit of configurability - one jest parameter which isn't supported by CRA, an extra webpack loader, or a different ESLint rule set. The easiest way to do this is to run `yarn eject`, unpacking all of what CRA hides away for you and dropping it in your project root for you to do with as you please. Unfortunately in doing this you lose the in-place updates with the latest tooling from Facebook, the configuration facade that lets you focus on development, and inevitably projects begin again to diverge.

### The Solution
The `create-react-app` repository is an example of a [monorepo](https://medium.com/@bebraw/the-case-for-monorepos-907c1361708a). It contains a number of packages within, each its own module and individually published, but all having some involvement in `create-react-app`. One of these packages is called `react-scripts`, and within it is all of the configuration and default project files included when you create a new CRA project. By forking the repo and publishing our own version of the `react-scripts` package we can take full control of these, without losing the benefits of using `create-react-app`.

If you use the forked scripts on a team, this also means that one person's improvements can benefit everybody - even those working on existing projects - and you'll still get all the new work from Facebook's end too.

### How tho
To fork the repo, open [it on github](https://github.com/facebookincubator/create-react-app) and hit "Fork" in the top-right (sign in if you haven't already). This will create a copy of the repository under the same name but in your github account. Now clone your forked repo somewhere, `cd` in to it and run `yarn`. There'll be a little more output than usual here while it sets up dependencies for the individual packages within the repo.

![Cloning the CRA repository and running yarn to install dependencies](clone-and-yarn.png)

Once the process completes, browse to `packages/react-scripts` in your editor. You'll see a few key files and folders inside.

* `config` - contains configuration for Jest, webpack builds and dev server
* `scripts` - this scripts available for running in a `create-react-app` project such as `yarn start` and `yarn build`
* `template` - the files you actually see when you've run `create-react-app` - the base of every new project
  * note the file `gitignore` instead of `.gitignore` - this is to avoid ignoring files from the template itself, but will be automatically renamed when generating a project

