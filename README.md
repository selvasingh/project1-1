<properties title="" pageTitle="NPMJS" description="Basic steps for creating and publishing packages to npm" metaKeywords="" services="" solutions="" documentationCenter="" authors="capfei" videoId="" scriptId="" manager="required" />

<tags ms.service="" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="05/21/2015" ms.author="capfei" />

# NPMJS #

This guide provides basic steps for creating and publishing scoped and unscoped packages to [npmjs.org](https://www.npmjs.org "https://www.npmjs.org") on Windows machines.

 - [Node.js and npm]
 - [Create a package from an existing GitHub repository]
 - [Publishing to npm]
 - [Scoped packages]


## Node.js and npm

Download and install Node.js and npm from [nodejs.org](https://nodejs.org/download/ "https://nodejs.org/download/").

Once Node.js has installed, run the Node.js command prompt. 
![](https://github.com/capfei/project1/blob/master/images/nodejs_command_prompt.PNG)

If you haven't created an npm account, you can create one at [npmjs.org](https://www.npmjs.org "https://www.npmjs.org") or by using the **`npm adduser`** command. If you already have an account, you can use  **`npm login`**. Both will prompt you for a username and password.


## Create a package from an existing GitHub repository

Creating a package from your GitHub repository is fairly simple. First, you will need to clone your repository locally through methods like GitHub for Windows or command line.

**GitHub for Windows:**

![] (https://github.com/capfei/project1/blob/master/images/GitHubWinClon.PNG)

**command line:**
```
git clone https://github.com/capfei/project1.git
```
To create the **`package.json`** file, in Node.js command prompt, **`cd`** into your repository then use the command **`npm init`**.
```bash
cd project1
npm init
```
This will prompt you to provide values for the **`package.json`** fields.
```bash
name: (project1)
version: (1.0.0)
description: Test
entry point: (index.js)
test command: 
git repository: (https://github.com/capfei/project1.git)
keywords:
author:
license: (ISC)
About to write to \project1\package.json:

{
	"name": "project1",
	"version": "1.0.0",
	"description": "Test",
	"main": "index.js",
	"scripts": {
		"test": "echo \"Error: no test specified\" && exit 1"
	},
	"repository": {
		"type": "git",
		"url": "git+https://github.com/capfei/project1.git"
	},
	"author": "",
	"license": "ISC",
	"bugs": {
		"url": "https://github.com/capfei/project1/issues"
	},
	"homepage": "https://github.com/capfei/project1#readme"
}

Is this ok? (yes) 
```
You can edit the **`package.json`** file to add any additionational fields needed. Please see [Specifics of npm's package.json handling](https://docs.npmjs.com/files/package.json "package.json") on the [npmjs.org](https://www.npmjs.org "https://www.npmjs.org").

Next, since I didn't specify my own entry point, the default is **`index.js`** and needs to be created. 
```javascript
//Simple function for a simple demo
module.exports = function () {
	console.log("Hello");	
};
``` 


## Publishing to npm

Once you have your package ready for the world to see, publish it to the npm registry with **`npm publish`** command . Don't forget to commit and push any changes to your repository. 
```bash
git add package.json index.js
git commit -m "add v1 package"
git tag 1.0.0
git push && git push --tags
```
*A tag was added to match the package version.*

Publish to the npm registry.
```bash
npm publish
```
Your package is now published and available on [npmjs.org](https://www.npmjs.org "https://www.npmjs.org").


## Scoped Packages

Creating a scoped package is similar to creating an unscoped package, except you will add the scope to the name when creating the **`package.json`** file.
```
@username/project-name
```
When publishing scoped packages, by default, they are private. Publishing private modules does require a paid account. You can publish public scoped modules for free by setting the access to public.
```bash
npm publish --access=public
```
If you have a paid account, you can publish private modules and change the access to public with the same **`access`** command or on [npmjs.org](https://www.npmjs.org "https://www.npmjs.org") in the 'Collaborators' section for the package.

![](https://github.com/capfei/project1/blob/master/images/npm_private_button.PNG)
```
https://www.npmjs.com/package/@username/project-name/access (for scoped packages)
or
https://www.npmjs.com/package/project-name/access (for unscoped packages)
```

<!--Anchors-->
[Node.js and npm]: #node.js-and-npm
[Create a package from an existing GitHub repository]: #create-a-package-from-an-existing-github-repository
[Publishing to npm]: #publishing-to-npm
[Scoped packages]: #scoped-packages
