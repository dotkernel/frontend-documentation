# NPM Commands

## Summary

This page installs the frontend build dependencies with npm and compiles the assets, either continuously while you develop or once, minified, for production.

## Details

> The Frontend interface has been tested with npm v10.0.4 and Node.js v20.11.0.

To install dependencies into the `node_modules` directory run this command.

```shell
npm install
```

> If `npm install` fails, this could be caused by user permissions of npm.
> The recommended way to install npm is through `Node Version Manager`.

The watch command compiles the components then monitors the files for changes and recompiles them.

```shell
npm run watch
```

After all updates are done, this command compiles the assets locally, minifies them and makes them ready for production.

```shell
npm run prod
```

To compile the assets once in development mode, without watching for changes, run:

```shell
npm run dev
```

## FAQ

### **Q: Where are the source assets, and where does the build write them?**

A: The sources are in `src/App/assets`.
Webpack writes the compiled files to `public/css`, `public/js`, `public/fonts` and `public/images`.

### **Q: Which Node.js and npm versions are supported?**

A: The interface has been tested with npm v10.0.4 and Node.js v20.11.0.

### **Q: Should I commit the compiled assets?**

A: The repository tracks the compiled `public/css/app.css` and `public/js/app.js`.
Run `npm run prod` before you commit asset changes so that the committed files are minified.
