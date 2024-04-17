#### Setup
1. Install [NodeJS](https://nodejs.org/en/)
2. Install [NVM](https://github.com/creationix/nvm)
3. (Optional if not installed) `nvm install 8.9.4`
4. Run `nvm use 8.9.4` or `nvm use`
5. Run `npm install`
6. Make sure `electron-packager` is globally installed. `npm install electron-packager -g`
7. Make sure `electron-installer-dmg` is globally installed. `npm install electron-installer-dmg -g`

#### Build
##### Preprare destination folder
Create `_app` folder structure beside your vaclient working directory.
```
_app    
└───builds/
└───installers/
│   └───darwin/
│   └───win32/
│       └───ia32/
│       └───x64/
vaclient
│package.json
|(etc)
```

!! IMPORTANT FOR BUILDING ON WINDOWS (NOT NEEDED FOR OSX) !!
Before building for windows, a file inside the `electron-wix-msi` node module needs to be fixed first. (No proper solution has been provided yet on Github)
- Go to `/node_modules/electron-wix-msi/lib` and open `creator.js`
- Search the method `getComponentId` at the bottom of the file and remove everything inside the function
and add a return statement `return ('a'+uuid()).replace(/-/g,'_');`
- That function should look like this.
```
getComponentId(filePath) {
    return ('a'+uuid()).replace(/-/g,'_');
}
```

##### Windows (recommended to use `Windows PowerShell`)
1. run `npm run cleanBuilds` -- this will delete old builds and installers
2. run `npm run win32` -- this will build for both and ia32 and x64 win32 architecture
3. run `npm run win32-make` -- this will create the installers for both ia32 and x64

##### Darwin (OSX)
1. run `npm run cleanBuilds` -- this will delete old builds and installers
2. run `npm run darwin` -- this will build create the build
3. run `npm run darwin-make` -- this will create the installer