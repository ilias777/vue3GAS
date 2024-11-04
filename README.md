# Vue3 with Google Apps Script

With this project your can use Vue3 with Google Sheets as a backend.

## Tools

#### Frontend

![Vue.js](https://img.shields.io/badge/vuejs-%2335495e.svg?style=for-the-badge&logo=vuedotjs&logoColor=%234FC08D)

#### Backend

![Google Apps Script](https://img.shields.io/badge/Google_Apps_Script-blue?style=for-the-badge&logo=google%20apps%20script&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google_Sheets-darkgreen?style=for-the-badge&logo=google%20sheets&logoColor=white)

#### Build tools

![Vite](https://img.shields.io/badge/vite-%23646CFF.svg?style=for-the-badge&logo=vite&logoColor=white)
![Clasp](https://img.shields.io/badge/CLASP-darkblue?style=for-the-badge&logo=google&logoColor=white)

> [!TIP]
> If you want to use a CSS framework like [DaisyUI](https://daisyui.com/) and [tailwindcss](https://tailwindcss.com/),
> you can see me other repo to use it &rarr; [here](https://github.com/ilias777/Vue3GASDaisyUI).

## Introduction

### Setup

#### Clone the repo:

```shell
git clone https://github.com/ilias777/vue3GAS.git
```

#### Navigate to the project folder:

```shell
cd vue3GAS
```

#### Install dependencies:

```shell
npm install
```

#### Remove the `.clasp.json` file in the root directory, to create later your own `.clasp.json` file with your scriptID:

```shell
rm .clasp.json
```

#### Install [clasp](https://github.com/google/clasp) in your system.

```shell
npm install -g @google/clasp
```

#### Create a Google Sheets Document.

- Go to [docs.google.com](https://docs.google.com/) and create a Google Sheets document
- Inside the Sheets document press in the menu bar, under extensions, _Apps Script_
- A new tab appears with the Google Apps Script code. **Copy the script ID** (https://script.google.com/macros/s/{scriptID}/edit).
- Press the `Deploy` button, in the upper right corner, to create a web app.

#### Enable Google Apps Script API

Go to [https://script.google.com/home/usersettings](https://script.google.com/home/usersettings)
and turn on the Google Apps Script API.

#### Login to your Google account from your terminal.

```shell
clasp login
```

Clone the Sheets script with clasp in the `./gas` folder.

```shell
clasp clone --rootDir ./gas <scriptID>
```

Move from the `./gas` folder the `.clasp.json` file to the root directory

```shell
mv ./gas/.clasp.json .
```

Build the project

```shell
npm run build
```

From here your can start build your web application, with Google Sheets as a backend.

If you are finish with your changes in your App, run `npm run build` to build the project and
a `index.html` are created in the `./dist` folder. Then this file is moved to the `./gas` folder
and all the files are pushed to google apps script automatically.

After the files are pushed, refresh the page of the Google Apps Script site, deploy your app again and you are done.

## How to

**These are the steps to reproduce the project:**

#### Create Vue Application:

```shell
npm create vue@latest
```

#### Navigate to your project directory:

```shell
cd <your-project-folder>
```

#### Install the node dependencies:

```shell
npm install
```

#### Delete unnecessary code for a clean project:

- Remove content from `./src/App.vue`.

```vue
<script setup></script>

<template>
  <h1>Hello from Vue</h1>
</template>
```

- Remove content from `./src/assets/main.css` and keep only the first line `@import './base.css';` In your `base.css` file you can add css styles if needed.

- Delete `./src/assets/logo.svg` file.

- Delete all folders and files from `./src/components/` folder.

#### Install Vue plugin for inline HTML, CSS and JavaScript:

```shell
npm install --save-dev vite-plugin-singlefile
```

#### Add the plugin in the `vite.config.js` file:

```javascript
import { viteSingleFile } from 'vite-plugin-singlefile'
export default defineConfig({
  plugins: [vue(), viteSingleFile()]
})
```

#### Install [clasp](https://github.com/google/clasp) in your system, to push the files to Google Apps Script

```shell
npm install -g @google/clasp
```

#### Create a Google Sheets Document

- Go to [docs.google.com](https://docs.google.com/) and create a Google Sheets document
- Inside the Sheets document press in the menu bar, under extensions, _Apps Script_
- A new tab appears with the Apps Script code. **Copy the scriptID**.

#### Connect the Google Sheets script to your project

Sing in to Google from your terminal with clasp.

```shell
clasp login
```

#### Enable Google Apps Script API

Go to [https://script.google.com/home/usersettings](https://script.google.com/home/usersettings)
and turn on the Google Apps Script API.

More information and the commands can you read in the [clasp repo](https://github.com/google/clasp)

#### Create a `./gas` folder in the root directory.

```shell
mkdir gas
```

#### Clone the Sheets script with clasp in the `./gas` folder.

```shell
clasp clone --rootDir ./gas <scriptUrl>
```

#### Move from the `./gas` folder the `.clasp.json` file to the root directory

```shell
mv ./gas/.clasp.json .
```

#### Pull the files from Apps Script:

```
clasp pull
```

Now you have in your `./gas` folder a `Code.js` file

#### Copy the following code inside this file:

```javascript
function doGet(e) {
  return HtmlService.createTemplateFromFile('index.html')
    .evaluate()
    .addMetaTag('viewport', 'width=device-width, initial-scale=1.0')
    .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)
    .setTitle('Vue3 GAS')
}
```

#### Push the files to Apps Script:

```shell
clasp push
```

#### Install Google types as a dependency:

```shell
npm install --save-dev @types/google-apps-script
```

#### Build the project to create a `./dist` folder:

```shell
npm run build
```

Copy `./dist/index.html` file to `./gas` folder

```shell
cp ./dist/index.html ./gas
```

#### Change build script command in `package.json` file:

```json
"scripts": {
    "build": "vite build && mv ./dist/index.html ./gas && clasp push",
}
```

Every change is saved in the `./dist/index.html` file. With the command `npm run build` the `index.html` file is copied in the `./gas`
folder and pushed to google apps script automatically.
