# Yarn vs npm

> Organizing things I couldn't explain precisely!
> Reference: [npm-vs-yarn-choosing-the-right-package-manager](https://medium.com/javascript-in-plain-english/npm-vs-yarn-choosing-the-right-package-manager-a5f04256a93f#:~:text=npm%20automatically%20executes%20a%20code,lock%20or%20package.)

<br>

<br>

### Before getting started

- Both npm and Yarn are excellent Node.js and JavaScript package managers
- So why was Yarn developed when npm already existed?
  - Yarn was created by Facebook to address npm's slow package installation speed and security issues
- In this article, we will compare these two package managers to help you decide which one to use

<br>

<br>

### 1. Parallel installation of packages

- When a single package is installed, a series of tasks are performed sequentially
- When installing multiple packages at the same time,
  - npm installs the next package only after the current one is fully installed
    - In other words, npm installs each package sequentially
  - On the other hand, Yarn processes these tasks **in parallel**, resulting in better **efficiency** and **speed**

<br>

As an example, when installing react with each package manager, the following results were observed:

- **npm** - 3.572 seconds
- **Yarn** - 1.44 seconds

Reference: [Yarn & npm benchmarks](https://github.com/pnpm/benchmarks-of-javascript-package-managers)

<br>

<br>

### 2. Automatic Lock file generation

- Both npm and Yarn manage dependencies through the **package.json** file
- You can notice that every time you install a new dependency, the version of the dependency starts with a **caret (^)** symbol
  - This means that every time we install a package, the package manager looks for a newer version
    - If a newer version exists, it installs the newer version instead of the version specified in the `package.json` file
  - If you don't want this behavior,
    1. Create a **lock file** to install a specific version, or
    2. Remove the **caret (^)** symbol
- Yarn automatically creates a `yarn.lock` file every time a new dependency is added
  - By storing the same version information at the time of package installation in the `yarn.lock` file, it helps ensure that the same versioned packages are installed when building a new environment
- npm can also create a lock file to fix dependency versions using the `npm shrinkwrap` command
  - However, the difference is that Yarn always creates and updates the `yarn.lock` file, whereas npm does not create a lock file by default and only updates the `npm-shrinkwrap.json` file when it already exists
  - Since npm v5.0, `package-lock.json` was introduced which contains **information about the dependency tree**, recording changes to `package-lock.json` whenever the `package.json` file or `node_modules` tree is modified using npm
    - This improved npm's package installation process and performance, but it still hasn't caught up with Yarn's speed

<br>

<br>

### 3. Security

- npm allows code to be executed immediately while installing packages, which can create security vulnerabilities
  - On the other hand, Yarn only installs files specified in `yarn.lock` or `package.json`, and because it installs fixed dependency versions through `yarn.lock`, it installs the same packages on all devices, making it safer than npm
- Yarn uses **checksums** to verify the integrity of installed packages before code is executed

<br>

<br>

#### Wrap-up

- Use Yarn for its speed, security, and reliability
