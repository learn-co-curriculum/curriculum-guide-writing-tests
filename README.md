You've written a fun, challenging lab, and now you need to test students'
results. So what do you do?

## Overview

Below, we'll document test approaches for various platforms. In each case,
we'll detail what the Learn platform expects in terms of test output so that
your tests run smoothly across students' environments.

1. [JavaScript](#javascript)
2. [Java](#java)

## JavaScript

### Mocha

If you're using [Mocha](http://mochajs.org/) to drive your test suite, you'll
simply need to make use of the JSON reporter and output its results to
`.results.json` in your lab's root directory. Normally, you could just add
the following command to the `scripts.test` entry in your `package.json`:

```bash
mocha -R json > .results.json
```

This approach will work just fine, but students won't see the results when they
run the tests unless they check the output file (which `learn-test` will delete
anyway, so they won't have much of a chance to open it). For this reason, we
recommend using [`mocha-multi`](https://www.npmjs.com/package/mocha-multi) until
[multiple reporter support](https://github.com/mochajs/mocha/pull/2091) is built
into Mocha.

You'll want to include `mocha-multi` in your `devDependencies`:
`npm install mocha-multi --save-dev`, and then you can run your tests with, for
example:

```bash
mocha -R mocha-multi --reporter-options spec=-,json=.results.json
```

## Java

Java testing is still a bit of a WIP, but for now the requirements are that
you expose an `ant test` target in your `build.xml` that outputs results as
XML. Your `test` target should probably make use of `clean` and `build` targets
to clean up previous builds and build a fresh project (respectively). 
