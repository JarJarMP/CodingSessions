## Today's goal
Using the previous session's [Docker image](https://github.com/JarJarMP/CodingSessions/blob/master/2015.08.18/DockerFile), install yeoman and with that create an application base.

## What is Yeoman?
Yeoman helps you to kickstart new projects, prescribing best practices and tools to help you stay productive. The workflow comprises three types of tools for improving your productivity and satisfaction when building a web app: the scaffolding tool (yo), the build tool (Grunt, Gulp, etc) and the package manager (like Bower and npm). [Read more about Yeoman](http://yeoman.io/)

## Let's get started
To install Yeoman, you need [nodejs](https://nodejs.org/) and [npm](https://www.npmjs.com/). I have it on my computer (container), so jump straight forward to yeoman installation:
```bash
$ npm install -g yo
```
Wasn't successful, we've recieved a warning message:
```bash
$ npm WARN engine yo@1.4.7: wanted: {"node":">=0.10.0","npm":">=2.8.0"} (current: {"node":"0.10.40","npm":"1.4.28"})
```
So the npm is a very old one, we need a newer version of it. We will install the required version:
```bash
$ npm install npm@2.8.0 -g
$ npm -v
2.8.0
```
Now, that we have the right version of npm, we can install yeoman:
```bash
$ npm install -g yo
> spawn-sync@1.0.13 postinstall /nodejs/lib/node_modules/yo/node_modules/cross-spawn/node_modules/spawn-sync
> node postinstall

Installing native dependencies (this may take up to a minute)
/nodejs/bin/yo -> /nodejs/lib/node_modules/yo/lib/cli.js

> yo@1.4.7 postinstall /nodejs/lib/node_modules/yo
> yodoctor

Yeoman Doctor
Running sanity checks on your system

✔ Global configuration file is valid
✔ No .bowerrc file in home directory
✔ NODE_PATH matches the npm root
✖ Node.js version

Your Node.js version is outdated.
Upgrade to the latest version: https://nodejs.org

✔ No .yo-rc.json file in home directory
✖ npm version

Your npm version is outdated.

Upgrade to the latest version by running:
npm install -g npm

Found potential issues on your machine :(

```
Hmm.. something fishy is going on here..

No worries, update them all! :)
```bash
$ npm install npm -g
$ npm -v
2.14.0

$ npm cache clean -f
$ npm install n -g
$ n stable

     install : node-v0.12.7
       mkdir : /usr/local/n/versions/node/0.12.7
       fetch : https://nodejs.org/dist/v0.12.7/node-v0.12.7-linux-x64.tar.gz
   installed : v0.12.7
```
There is nothing between us and the yeoman:
```bash
$ npm install -g yo
 
> spawn-sync@1.0.13 postinstall /usr/local/lib/node_modules/yo/node_modules/cross-spawn/node_modules/spawn-sync
> node postinstall

/usr/local/bin/yo -> /usr/local/lib/node_modules/yo/lib/cli.js

> yo@1.4.7 postinstall /usr/local/lib/node_modules/yo
> yodoctor


Yeoman Doctor
Running sanity checks on your system

✔ Global configuration file is valid
✔ NODE_PATH matches the npm root
✔ Node.js version
✔ No .bowerrc file in home directory
✔ No .yo-rc.json file in home directory
✔ npm version

Everything looks all right!
```
As the man says int he console, everything looks all right! Yaaay! :)

Quick test, just to make sure:
```bash
yo -v

/usr/local/lib/node_modules/yo/node_modules/configstore/index.js:46
				throw err;
				      ^
Error: EACCES, permission denied '/root/.config/configstore/insight-yo.json'
You don`t have access to this file.

    at Error (native)
    at Object.fs.openSync (fs.js:500:18)
    at Object.fs.readFileSync (fs.js:352:15)
    at Object.create.all.get (/usr/local/lib/node_modules/yo/node_modules/configstore/index.js:27:26)
    at Object.Configstore (/usr/local/lib/node_modules/yo/node_modules/configstore/index.js:20:44)
    at new Insight (/usr/local/lib/node_modules/yo/node_modules/insight/lib/index.js:37:34)
    at Object.<anonymous> (/usr/local/lib/node_modules/yo/lib/cli.js:130:15)
    at Module._compile (module.js:460:26)
    at Object.Module._extensions..js (module.js:478:10)
    at Module.load (module.js:355:32)
```
And this went on for 2 hours long.. 

We couldn't solve it, after reading all the stackoverflow-githubissue-googlesearch results.. :(

But we wanted to build at least one base with yeoman, so we did it on our host machines:
```bash
$ npm install -g yo grunt-cli bower generator-angular-fullstack
$ yo angular-fullstack app0827
```

Next time we will create a Docker image with nodejs from an Ubuntu image, and try yeoman with that way. Hopefully it will go better than this... :)