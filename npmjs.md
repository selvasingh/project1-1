<properties title="" pageTitle="NPMJS" description="Basic steps for creating and publishing packages to npm" metaKeywords="" services="" solutions="" documentationCenter="" authors="capfei" videoId="" scriptId="" manager="required" />

<tags ms.service="" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="06/22/2015" ms.author="capfei" />

# NPMJS #

This guide provides basic steps for creating and publishing scoped and unscoped packages to [npmjs.org] on Windows machines.

 - [Node.js and npm]
 - [Create a package from an existing GitHub repository]
 - [Publishing to npm]
 - [Scoped packages]


## Node.js and npm

Download and install Node.js and npm from [nodejs.org].

Once Node.js has installed, run "Node.js command prompt". 
![][nodejs command prompt]

If you haven't created a npm account, you can create one at [npmjs.org] or by using the **`npm adduser`** command. If you try to create an account with a username already in use, you will get an error.  

Use the **`npm login`** command, if you already have an account. Both `adduser` and `login` will prompt you for a username, password and email address.

Next, check to make sure the package name you want to use is not already taken. 
```bash
npm view package-name
```
If the name is not taken, you will an error message:
```bash
npm ERR! 404 'package-name' is not in the npm registry.
```
If it is taken, the contents of the **`package.json`** file will be listed. 

You can also check name availability with https://registry.npmjs.org/ and typing https://registry.npmjs.org/ adding the name you wish to use in the address bar of your web browser. 

Example:
```
https://registry.npmjs.org/package-name
```
If the name is taken, the contents of the **`package.json`** will be listed. Otherwise, you will get an error page. 

Node.js command prompt does not have `git` commands available by default. You will need to run a separate command-line client like GitShell or use a GUI like [GitHub for Windows].


## Create a package from an existing GitHub repository

Creating a package from your GitHub repository is fairly simple. First, you will need to clone your repository locally through methods like [GitHub for Windows] or command-line.

**GitHub for Windows:**

![Clone in GitHub Windows][GitHubWinClon]

**command-line:**
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
name: (project1) capfei-project1
version: (1.0.0)
description: Test
entry point: (index.js)
test command: 
git repository: (https://github.com/capfei/project1.git)
keywords:
author: capfei
license: (ISC)
About to write to \project1\package.json:

{
	"name": "capfei-project1",
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
You can edit the **`package.json`** file to add any additionational fields needed. Please see [Specifics of npm's package.json handling] on the [npmjs.org].

Next, since I didn't specify my own entry point ([main]), the default is **`index.js`** and needs to be created. This file will be loaded when your module is required. 
```javascript
//Simple demo function
module.exports = function () {
	console.log("Hello");	
};
``` 


## Publishing to npm

Before publishing your package, you will need to commit and push any changes to your repository. 

**command-line:**
```bash
git add package.json index.js
git commit -m "add v1 package"
git tag 1.0.0
git push && git push --tags
```
*A [tag] was added to match the package version.*

To do the same process in [GitHub for Windows], you will first need to [commit your changes] then follow the steps on [creating a release]. You can use an existing tag or create a new one to add to a branch or a specific commit.

Once you have your package ready for the world to see, publish it to the npm registry with **`npm publish`** command.
```bash
npm publish
```
Your package is now published and available on [npmjs.org].

![][published]


## Scoped Packages

Creating a [scoped package] is similar to creating an unscoped package, except you will add the scope to the name when creating the **`package.json`** file.
```
@username/name
```
Example:
```
@capfei/project1
```
When publishing scoped packages, by default, they are private. Publishing private modules does require a paid account. You can publish public scoped modules for free by setting the access to public.
```bash
npm publish --access=public
```
If you have a paid account, you can publish [private modules] and change the access to public with the same **`access`** command or on [npmjs.org] in the 'Collaborators' section for the package.

![][npm private setting]
```
https://www.npmjs.com/package/@username/name/access (for scoped packages)
or
https://www.npmjs.com/package/name/access (for unscoped packages)
```

<!--Anchors-->
[Node.js and npm]: #node.js-and-npm
[Create a package from an existing GitHub repository]: #create-a-package-from-an-existing-github-repository
[Publishing to npm]: #publishing-to-npm
[Scoped packages]: #scoped-packages

<!--Links-->
[npmjs.org]: https://www.npmjs.org "npmjs.org"
[nodejs.org]: https://nodejs.org/download/ "https://nodejs.org/download/"
[nodejs command prompt]: https://github.com/capfei/project1/blob/master/images/nodejs_command_prompt.PNG "Node.js command prompt"
[GitHub for Windows]: https://windows.github.com/ "GitHub for Windows"
[GitHubWinClon]: https://github.com/capfei/project1/blob/master/images/GitHubWinClon.PNG
[Specifics of npm's package.json handling]: https://docs.npmjs.com/files/package.json "package.json"
[main]: https://docs.npmjs.com/files/package.json#main "package.json#main"
[tag]: http://git-scm.com/book/en/v2/Git-Basics-Tagging "Git Basics - Tagging"
[commit your changes]: https://help.github.com/articles/synchronizing-repositories/ "GitHub for Windows - Synchronizing repositories"
[creating a release]: https://help.github.com/articles/creating-releases/ "GitHub - Creating Releases"
[published]: https://github.com/capfei/project1/blob/master/images/published.PNG "Published"
[scoped package]: https://docs.npmjs.com/misc/scope "npm - Scoped packages"
[private modules]: https://www.npmjs.com/private-modules "npm Private Modules"
[npm private setting]: https://github.com/capfei/project1/blob/master/images/npm_private_button.PNG "private setting"
