[package-managers]: https://github.com/topics/package-manager
[facebook-launches-yarn-a-faster-npm-client]: https://thenextweb.com/dd/2016/10/12/facebook-launches-yarn-a-faster-npm-client/
[npm-yarn-express-install]: https://www.sitepoint.com/yarn-vs-npm/
[facebooks-yarn-vs-npm-is-yarn-really-better]: https://medium.com/@nikjohn/facebooks-yarn-vs-npm-is-yarn-really-better-1890b3ea6515
[npm-v5-3-0-vs-yarn-0-27-5-speed]: https://blog.oharagroup.net/npm-v5-3-0-vs-yarn-0-27-5-speed-c9d3be07b557
[npm-github]: https://github.com/npm/npm
[yarn-github]: https://github.com/yarnpkg/yarn

# introduction
We all use packange managers to get our work done.  In the Front End space, npm has been the defacto standard for a while.  There is a new kid in town, and that is Yarn.


# package managers
>A package manager is a set of tools that automates and manages computer software. They deal with packages, or collections, of bundled files. Package managers make it easy to install, upgrade, or remove software for a computer's operating system - _[Package Managers - Wikipedia][package-managers]_

- npm
- yarn
- bower
- bundler
- aptitude
- yum
- homebrew


# npm vs yarn on github
| |[npm][npm-github]|[yarn][yarn-github]|
---:|:---:|:---:|
version|5.5.1|1.2.1|
watchers|774|551|
stars|14,253|28,288|
forks|2,812|1,492|
install|packed with node|`brew install yarn`|


# npm
Node Package Manager is packaged with `Node`

## features
- Installs packages synchronously from `http://registry.npmjs.org`
- `npm install` installs, in serial, dependencies and creates a `package-json.lock` file
- Verbose output post-install
- Allows installs from private repos


# yarn
Yarn was developed by engineers from Facebook, Exponent, Google, and Tilde to solve.  Facebook had used npm extensively for numerous projects, but had trouble scaling it for internal use as it posed issues with performance and security _([facebook-launches-yarn-a-faster-npm-client][facebook-launches-yarn-a-faster-npm-client])_.

## features
- `yarn install` installs, in parallel, only dependencies listed in `yarn.lock`, or `package.json` if `yarn.lock` does not exist
- Caches every download
- Allows for offline installs as long as the package has been installed before
- Flat mode resolve mismatching versions of dependencies to a single version to avoid creating duplicates _([facebooks-yarn-vs-npm-is-yarn-really-better][facebooks-yarn-vs-npm-is-yarn-really-better])_
- A single request failing won’t cause an install to fail. Requests are retried upon failure _([facebooks-yarn-vs-npm-is-yarn-really-better][facebooks-yarn-vs-npm-is-yarn-really-better])_
- `yarn licenses` provides a group of commands for investigating dependency licenses
- `yarn why` allows you to peek into the dependency graph to figure out why a given package is installed


# how to use yarn
- install project dependencies: `yarn`
- add a package: `yarn add PACKAGE_NAME`


# performance
Yarn is generally faster except when there is no lockfile or cache _([npm-v5-3-0-vs-yarn-0-27-5-speed][npm-v5-3-0-vs-yarn-0-27-5-speed])_

With the `Express Generator` using the following commands:
```bash
npm install express-generator -g
express myapp
npm install
```

- npm average is **188.216 sec**
- yarn average is **39.222 sec**

_copied from tests performed here: [Facebook’s Yarn vs npm — Is Yarn really better?][facebooks-yarn-vs-npm-is-yarn-really-better]_


# should I use?
Maybe?

- Yarn creates it's own lockfile and will read from the same `registry.npmjs.org` as npm.
- On initial project installs, Yarn is mostly faster than npm.  However, if there is no internal cache or lock file, the install speed differences are fairly insignificant.
- If your network connection is spotty, Yarn can handle spotty network conditions better than npm
- `yarn --verbose` provides much more information about what is happen than `npm install --verbose`
- You _could_ use yarn on projects, but this will introduce a separate lockfile that users of npm will not be able to read, thus defeating it's purpose
- Yarn provides some additional tools like `yarn licenses` and `yarn why`


# conclusion
When I started this research, I was convinced that Yarn was a clear winner.  However, Npm 5 has added most of the features that Yarn aimed to add/improve.  The big one being support for deterministic installs with the use of a `package-json.lock` file.  If speed is a major concern, Yarn may be the way to go.  Yarn is going to be faster in most cases, but not all.

# reference
- [package-managers][package-managers]
- [facebook-launches-yarn-a-faster-npm-client][facebook-launches-yarn-a-faster-npm-client]
- [npm-yarn-express-install][npm-yarn-express-install]
- [facebooks-yarn-vs-npm-is-yarn-really-better][facebooks-yarn-vs-npm-is-yarn-really-better]
- [npm-v5-3-0-vs-yarn-0-27-5-speed][npm-v5-3-0-vs-yarn-0-27-5-speed]
- [npm-github][npm-github]
- [yarn-github][yarn-github]
