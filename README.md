## Mini-Projects - Proxi Week 1

For the first week, we want students working on 2-5 smaller projects.  These will all be command-line projects and the focus is on writing clean, well-tested code.

Each project is small enough that you can make good progress in 2-5 hours.  They are also the kind of project you might be asked to write in an interview.

Each project will have suggestions about structure and iterations, but we want you all making most of the decisions (what classes, what functions, what files, how to structure, etc.).  For that reason, the projects are outlined more briefly than the text-analysis project.

This is also more similar to what you'd see in an interview if you were asked to build one of these projects.

You are free to write the project in any language you choose.  Do most of the projects in JavaScript, but doing one of these projects in another language is a good way to dive into that language.

What we ask:

1. The work on each project is broken down into multiple, easy-to-review pull requests
1. The code follows AirBnb's JavaScript style guide or the equivalent if you use another language
1. The code has well-written automated tests

To get started on a project:

1. Find the description in this repository
1. Create a repository of your own
1. Add the Proxi instructors as collaborators on that project
1. Submit pull requests and request reviews as you make progress

In Monday's group session, we will start on one project together.  In the next group session, we will have people demo one of the projects they've worked on.

## Configuring Projects w/ Jest + ESLint

If you're using VS Code, Atom, or similar, install the `eslint` extension.

### Jest

Relevant documentation:
- [Getting Started with Jest](https://jestjs.io/docs/en/getting-started)
- [Configuring Jest](https://jestjs.io/docs/en/configuration)

By default, Jest expects all tests to live in the `__tests__` directory.

To install `jest`, run

```console
npm install --save-dev jest
```

To create a `jest` configuration file, run

```console
jest --init
```

and follow the instructions.

If you want `npm test` to run `jest`, edit the `"scripts"` section in `package.json`:

```json
{
  "scripts": {
    "test": "jest"
  }
}
```

### ESLint w/ AirBnb's Style Guide

We're using [AirBnb's JavaScript Style Guide](https://github.com/airbnb/javascript), mostly to get used to using a style guide and a linter that enforces the style.

To install in your project, run

```javascript
npx install-peerdeps --dev eslint-config-airbnb-base
```

Edit `.eslintrc.json` so it extends the `airbnb-base` rules:

```json
{
  "extends": "airbnb-base",
  "rules" :{
    "no-console": "off"
  }
}
```

If you're writing a command-line app we recommending setting the `no-console` rule to `"off"`, since using `console.log` in the command-line context is fine.

### ESLint w/ Jest

By default, ESLint doesn't like the Jest test files.  Install the following plugin:

```console
npm install --save-dev eslint-plugin-jest
```

Tell ESLint to ignore your Jest configuration file by adding this line to the `.eslintignore` file:

```text
jest.config.js
```

Edit `.eslintrc.json` so `eslint` knows what to do when looking at Jest test files:

```json
{
  "env": {
    "jest/globals": true
  },
  "extends": "airbnb-base",
  "plugins": ["jest"],
  "rules" :{
    "no-console": "off"
  }
}
```
