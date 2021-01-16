If you are a Node.js developer, you must have used NPM in one or many instances when developing your Node.js app. NPM is buddle with Node.js. If you install Node.js on your computer, you get NPM. NPM was initially released back on [12th January 2010](https://en.wikipedia.org/wiki/Npm_(software)). It has gained tremendous fame among JavaScript developers. It helps to install Node.js packages and modules and later run them as if they were built-in. With the progressive growth of Node.js, NPM has introduced a new tool called NPX. Although NPX is bundled with NPM, they both treat packages differently. This guide will help you learn and contrast the difference between NPM and NPX.

### What is NPM

NPM is the Node Package Manager. It's pre-installed with Node.js. It makes it easier for developers to share and reuse open source code by enabling them to install open source modules. Modules are JavaScript packages that you install in your system using NPM. NPM helps to manage packages in your projects as dependencies.

### What is NPX

[NPX](https://www.npmjs.com/package/npx) is an NPM package Executor. Initially, NPX was launched in [July 2017](https://nodejs.dev/learn/the-npx-nodejs-package-runner). NPX was just an NPM package that could be installed like other NPM packages. Currently, NPX is bundled with NPM when you install the NPM version 5.2.0 or higher.

### How NPM treat Node.js packages

It sets up modules such that Node.js can locate the packages and manage the dependencies of that application intelligently.

When using NPM, there are two ways to install a package into your local computer.

- Locally: When a package is installed locally, It is installed in `./node_modules/.bin/` of the local project directory.

- Globally: A global package is installed in the user environment path. `/usr/local/bin` for Linux and `AppData%/npm` for Windows.

When you install executables using NPM, Node.js links them either from the local or global path. As a package manager, NPM does not execute a package directly.

To use and run an NPM installed package, you should specify the package is the `package.json` file. It is created automatically when you initialize your first Node.js project with `npm init -y`.

To execute a locally installed package, it must be specified in the package.json scripts scaffold as shown below.

```bash
"scripts": {
    "your-package":  "your-package-name"
},
```

Then execute with

```bash
npm run your-package-name
```

On the other hand, you can type the package path in a command-line tool.

For example, let’s say you have installed [Eslint](https://www.npmjs.com/package/eslint), a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code.

```bash
npm install eslint
```

To execute the package binaries, you have to point to the package path.

```bash
./node_modules/.bin/your-package-name
```

```bash
./node_modules/.bin/eslint --init
```

And provide the argument to execute

```bash
./node_modules/.bin/eslint yourfile.js
```

NPX comes in to solve a couple of keystrokes to make it easier to execute Node.js modules. It makes it easier to run and interact with executables hosted in the NPM registry and to execute NPM local binaries. It also comes with many added features.
### Using NPX

With NPX, you can run and execute packages without having to install them locally or globally.

When running NPM executables with NPX, if a package is installed, NPX will search for the package binaries (either local or global) and then run the package.

If the package is not installed, executes the package directly from the NPM registry without locally saving the package binaries. It will execute the package binaries without installing the packages in your system, as you would typically do with NPM.

Let's check some key use cases of NPX.

Run the following command to make sure you have NPX installed using `which npx`.

If not installed, use `npm install -g NPM@latest` to update NPM to the higher version above 5.2 or later, and you will have the NPX CLI tool available. You can also install NPX as a stand-alone package. Run `npm i npx` to install the NPX runner.

#### NPX standard command

To execute a package with NPX, run:

```bash
npx your-package
```

Type `npx --help` to get a more detailed npx commands syntax.

Output:

```bash
npx [options] <command>[@version] [command-arg]...

npx [options] [-p|--package <package>]... <command> [command-arg]...

npx [options] -c '<command-string>'
```

#### Executing installed packages

When using NPM, you had to remember and type the path of the package in the command, as explained in the Eslint case.

```bash
./node_modules/.bin/eslint yourfile.js
```

It is tiresome to always add the node modules path, referencing them all over your files and commands.

With NPX, you can have your local packages installed and use NPX commands (instead of adding the whole path) to execute the package binaries.

```bash
npx eslint yourfile.js
```

NPX lets you execute local 'node_modules' as if they were global. If the package was not previously installed, NPX would not install the package in your system; instead, it will create a temporary cache that will hold the package binaries. Once the execution is over, NPX will remove the installed cache binaries from the system. This way, your globals stays clean. This saves on disk size and allows you to run a package only when it's needed. It also gives you the advantage of testing packages without having to install them.

This concept is commonly seen when executing NPM scripts. For example, let's say you are using the [Sequelize](https://sequelize.org/) package to automate data migration and seed data from your project. For that case, you will need the [Sequelize CLI](https://www.npmjs.com/package/sequelize-cli). You will need to know where Sequelize is installed in your project in order to execute the package binaries. For example

```bash
node_modules/.bin/sequelize
```

Using NPM is pretty easy, as you just need to edit the `package.json` script and add the package path.

```bash
"scripts": {
    "db:migrate" 'node_modules/.bin/sequelize db:migrate'
},
```

To seed the database, execute the script by running

```bash
npm run db:migrate
```

This is not that hard.

However, when you use NPX, things get very much simpler.

Running the below command will be enough to seed the database.
Why NPX over NPM scripts.

```bash
npx sequelize db:seed
```

- No need to edit the `package.json` file with `node_modules` paths.
- You can directly execute the tool from the command line.

#### One-off commands

NPX treats global packages differently. Global packages are commonly used for development purposes. For that reason, you don’t need them installed all the time. NPX helps to execute these packages only when you need them. This comes in hand, as many global packages are one-off commands.  You only need to run them once.

For example, to create a [React](https://create-react-app.dev/docs/getting-started/) boilerplate app with NPM, you need to install the [React](https://www.npmjs.com/package/create-react-app) module and then create an app with `npm init react-app my-app`. This means that when you need to create another React app in features, chances are you will create an app using the executables that you installed previously. This rule you out of newly updated features under this package unless you update the package manually.

Using NPX, you will only run the command once without installing the package.

```bash
npx create-react-app my-sample-app
```

With NPX, one-off commands such as this are a lot more simple and straightforward. You need to run an NPX command once, and the app is created under the directory where the command line point. And when you need to create another React app, you just run the NPX command repeatedly without installing the package on your local computer. You don't need to worry about the package updates, as NPX will always fetch the latest version available in the NPM registry. With such approaches, you avoid clogging up your globals with packages that you use once in a blue moon.

#### NPX versioning

When it comes to packages versioning, NPM will handle that perfectly with its `package-lock.json` file. With NPX, there are a lot more features that you can benefit from package versioning, such as

- Executing a specific package version.

If you want to execute a specific package's version, let's say, Eslint, you should specify the package version, as shown below.

```bash
npx eslint@3.9.0 --version
```

Your project will be executed with the package version you have specified.

- Version testing.

With NPM, if you want to test packages, you have to download the packages and run them inside your project. This comes in handy when upgrading packages to newer versions. With NPX, you can check out the new version before deciding whether to update them to determine if the new version is compatible with your project.

NPX plays a great role in testing new package versions with your project before integrating them into your project. You can check out the latest version before you decide whether to upgrade your project or not.

For example, let's take a Node.js project, for instance where [Webpack](https://www.npmjs.com/package/webpack) is installed globally, and the currently installed version is 4.40.3. Webpack is used for bundling project assets. Check out this [guide](/engineering-education/webpack/) to learn more about configuring Webpack with your project. When configured, run `webpack` to get the command results.

```bash
Hash: b41ed73s02F90S74F9b
Version: webpack 4.40.3
Time: 394ms
        Asset     Size  Chunks             Chunk Names
    build/main.js   7.32 kB       0  [emitted]  main
   [0] ./index.js 4.02 kB {0} [built]
```

Let's try using NPX and run webpack at version 5.11.1 to see what the difference would look like on the project. Run `npx webpack@5.11.1`.

```bash
Hash: b41ed73s02F90S74F9b
Version: webpack 5.11.1
Time: 379ms
        Asset     Size  Chunks             Chunk Names
    build/main.js   5.62 kB       0  [emitted]  main
   [0] ./index.js 4.02 kB {0} [built]
```

Here, the results show that the new version will help you buddle your project further with a couple of KBs.

- NPX with NVM

[NVM](https://dev.to/ms314006/how-to-install-NPM-through-nvm-node-version-manager-5gif) stands for Node Version Management. It helps you to install different Node.js versions is your computer.

Moving a Node.js installation from one version to another using [NVM](https://dev.to/ms314006/how-to-install-NPM-through-nvm-node-version-manager-5gif) can be a little bit tricky. NPX helps you to use specific Node.js versions without using NVM.

For example

```bash
npx -p node@12.18.3 -- node index.js
```

You can use the version to run your .js files. This becomes useful when checking the different new features added in Node.js versions.

#### Execute Code from URL such as gist

NPX will download and run the code directly from a gist.

Here is a simple example of running a gist code. The gist has the `main.js` and `package.json` files.  Let's see the NPX output. Check the code from the [Github gist](https://gist.github.com/kimkimani/116e1e9d898169662fbaf6973bdbc3f5).
Then run

```bash
npx https://gist.github.com/kimkimani/116e1e9d898169662fbaf6973bdbc3f5
```

NPX will point to the remote `.js` file, download it temporarily, execute it and give you the result to your console.

![Execute Gist Code with NPX](/engineering-education/npm-vs-npx-what-is-the-difference/execute-gist-code-with-npx.jpg)

Note, it is advisable to take precautions when executing any remote files you don't own. Always check the code before executing the files. This way, you avoid been trapped into malicious code.

### Final notes

NPX is a great tool that you should try out. It will help you to avoid NPM dependencies and versioning. Above all, you get to execute packages without having to install them.

Here is some common comparison summary between NPX and NPM

#### Comparison summary

| NPM | NPX |
|-|-|
| It is a Node.js package manager. Used to install, update, and manages package dependencies. | It is a Node.js package executer. It is used to execute Node.js packages binaries. |
| NPM is pre-installed with Node.js. When you install Node.js, you get NPM installed .| NPX binaries executors are bundled with NPM. When you install NPM version 5.2.0 or higher, get NPX installed. Or you can install NPX as a stand-alone with `npm i npx`. |
| For NPM to execute a package, you have to install the package from the NPM registry into your system. | NPX executes packages without necessarily having previously installed the package. |
| When executing a package, it will look for the package binaries either from the local or global installation. If not found that the end and no package will be executed. | When executing a package, it will look for them either in the local or global path. If the package is no found, NPX will take a step further. It will download and store the package binaries temporarily and then execute the package. When the execution is over, NPX will do away with the install. |
| For NPM to use a package, it has to be specified in the `package.json` under the script fold or available in the package's executable path. | No much hustle with editing the package.json script or remembering the package path. NPX executes packages directly from the NPM registry if not available on your local machine. |
| Due to package versioning of the NPM `package-lock.json` file, you must update the package to the latest version to use the latest updated package version. | You don't have to update and installed the package to take advantage of new update features or bug fixes. NPX will always execute the latest available version in the NPM registry. And if you need to run a specific package version, you specify the version in the NPX command, and NPX will handle the versioning for you. |

I hope this guide helped you understand the differences between NPM and NPX and understand some major use cases of NPX.