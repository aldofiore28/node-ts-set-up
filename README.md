# **How to set up Node + Typescript project**

* `npm init` to initialize a package.json. `npm init -y` to answer yes to all the questions at CLI set up.
* `npm i -D typescript` to install typescript as a dev dependency.
* `npx tsc --init` to initialize the tsconfig.json. This is a set of instructions that the Typescript compiler will follow when compiling the code, removing the need to pass those in every time we want to compile code.
  * you can customize this file as you wish.
* Install all the needed packages
  * Some basic packages:
    * `dotenv` loads a local `.env` file into `process.env` to access them in the code easily
    * `rimraf` cross-platform `rm -rf` to remove `build` folder before new build.
    * `express` to set up an API
    * `helmet` sets some security http headers in the express app
    * `cors` enables cors in the express app
  * For development:
    * `nodemon` tool to restart the node app when file changes in the directory are detected
    * `concurrently` runs commands concurrently
  * Remember to bring in the `@types/*` packages when not implemented by the package itself
* Create npm scripts to run and develop the app locally
```
"scripts": {
    "build": "rimraf build && tsc", // removes the build folder and recompiles typescript
    "predev": "npm run build", // command that happens before the `dev` command. Invokes `npm run build`
    "dev": "NODE_ENV=development concurrently \"tsc --watch\" \"nodemon -q build/index.js\"", // sets the node env to development and runs concurrently the TS compiler in watch mode and nodemon to restart the application when the files in the build folder change
    "prestart": "npm run build", // command that happens before the `start` command. Invokes `npm run build`
    "start": "NODE_ENV=production node build/index.js", // builds a production version of the app
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  ```