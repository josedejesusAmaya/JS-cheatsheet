### NPM Basics
Node Package Manager to install dependencies.
Dependencies are packages that are used in all of your projects and come with a package.json file. This file is the map of your project.

### Adding packages locally or globally
#### Locally
It is installed in your project's directory.

#### Globally -g or -global
It is installed in your system available to all projects.

### What exactly are dev dependencies?
It basically tells npm to install these as dev tools. Wich means they won't be included in your production bill, but used throughout development.
So when you compile the production bill, these dependencies won't be included.

Check for updates of our locally dependencies
```
	npm outdated
```
Use -g to check dependencies globally

#### To update a package
```
	npm update name
```
Or use the install command again

#### How to remove a package?
```
	npm uninstall name
```

### Semantic Versioning
1.4.2
* Major new releases: Like a full new version of a software.
* Minor releases: Like adding new functions to this major release or a new tool.
* Patch relseases: The last number are patches and fixies, usually for bugs and such.

Caret										->  ^1.x.x
All minor and patches OK

Tilde										-> ~1.5.x
All patches only

- `^version` **“Compatible with version”**, will update you to all future minor/patch versions, without incrementing the major version. `^2.3.4` will use releases from 2.3.4 to <3.0.0.
-   `~version` **“Approximately equivalent to version”**, will update you to all future patch versions, without incrementing the minor version. `~1.2.3` will use releases from 1.2.3 to <1.3.0.

### package-lock.json
When we do NPM install, the package.json file is the input, and the package-lock.json is the output. And this file will guarantee the same install, every time we do an NPM install, wherever we pass this project to. As long as we commit the package-lock.json file to our repo, or when you pass this project along to someone make sure to included.

### Manage your cache
```
	npm cache verify
	npm cache clean --force
```

### NPM Audit
```
	npm audit
```

### Scripts
For preloaded commands:
```
	npm script
```

For our custom scripts:
```
	npm run script
```

### NPX
Install temporarily Angular:
```
	npx -p @angular/cli ng new myapp
	npx mocha
	npx cowsay hello!
```
-p for package
Then use a command from that package to create a new app.

### Yarn is the alternative for NPM
By FB and usually faster.

### Requirements for publishing
- npm account
- Well-documentated README file
- Scoped package name: unique, descriptive, meetd npm policies (example: @angular/cli or @angular/core).
- Unscoped: not owned already. spelled similary, confusing (example: Reack or Redux).

### Dist-Tags
Are human readable tags you can add when your publish your packages to NPM.
You can add details with tags that will be descriptive of this version
- Easy way to clarify details around release.
- Used when publish packages with --tag.
```
	npm publish --tag bugfix
```
- Used after publication with dist-tag command
```
	npm dist-tag add test-npm@1.0.0 [stable]
```

### How to publish?
1. Make npm login.
	```
		npm login
	```
2. Create your project.
	```
		npm init
	```
3. Add README.md file in the root folder
4. Publish.
	```
		npm publish --tag beta
	```
5. After modifications and before publish again you must change the semantic version in your package.json file.

### How to publish a scope package
You need to have a paid accound for private packages.
By default scope packages are publish as private.

1. Create your project:
	```
		npm init --scope=company-name
	```
2. Add a tag and publish it.

### How to publish public scope packages
```
	npm publish --access public
```

### How to use your own package
1. Ensure that you are login into your account.
2. 
```
	npm install @company/package
```