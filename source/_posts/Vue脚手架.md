Vue脚手架

```ruby
Last login: Fri Apr 24 09:31:11 on console
 l@ls-MacBook-Air  ~  npm -v
6.14.4
 l@ls-MacBook-Air  ~  webpack -v
3.6.0
 l@ls-MacBook-Air  ~  npm install -g @vue/cli
npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
npm WARN deprecated fsevents@1.2.12: fsevents 1 will break on node v14+. Upgrade to fsevents 2 with massive improvements.
/usr/local/bin/vue -> /usr/local/lib/node_modules/@vue/cli/bin/vue.js

> fsevents@1.2.12 install /usr/local/lib/node_modules/@vue/cli/node_modules/fsevents
> node-gyp rebuild

  SOLINK_MODULE(target) Release/.node
  CXX(target) Release/obj.target/fse/fsevents.o
  SOLINK_MODULE(target) Release/fse.node

> core-js@3.6.5 postinstall /usr/local/lib/node_modules/@vue/cli/node_modules/core-js
> node -e "try{require('./postinstall')}catch(e){}"

Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!

The project needs your help! Please consider supporting of core-js on Open Collective or Patreon:
> https://opencollective.com/core-js
> https://www.patreon.com/zloirock

Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)

+ @vue/cli@4.3.1
added 100 packages from 50 contributors, removed 18 packages, updated 228 packages and moved 7 packages in 102.781s
 l@ls-MacBook-Air  ~  vue --version
@vue/cli 4.3.1
 l@ls-MacBook-Air  ~  npm install -g @vue/cli-init
npm WARN deprecated vue-cli@2.9.6: This package has been deprecated in favour of @vue/cli
npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
npm WARN deprecated coffee-script@1.12.7: CoffeeScript on NPM has moved to "coffeescript" (no hyphen)
+ @vue/cli-init@4.3.1
added 254 packages from 207 contributors in 19.423s
 l@ls-MacBook-Air  ~  cd /Users/l/Desktop/VueTemp/vueDemo
 l@ls-MacBook-Air  ~/Desktop/VueTemp/vueDemo  vue init webpack vuedemo001

? Project name vuedemo001
? Project description test vue demo 001
? Author ifeiyv 719507339@qq.com
? Vue build standalone
? Install vue-router? No
? Use ESLint to lint your code? No
? Set up unit tests No
? Setup e2e tests with Nightwatch? No
? Should we run `npm install` for you after the project has been created? (recommended) npm

   vue-cli · Generated "vuedemo001".


# Installing project dependencies ...
# ========================

npm WARN deprecated extract-text-webpack-plugin@3.0.2: Deprecated. Please use https://github.com/webpack-contrib/mini-css-extract-plugin
npm WARN deprecated browserslist@2.11.3: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
npm WARN deprecated bfj-node4@5.3.1: Switch to the `bfj` package for fixes and new features!
npm WARN deprecated core-js@2.6.11: core-js@<3 is no longer maintained and not recommended for usage due to the number of issues. Please, upgrade your dependencies to the actual version of core-js@3.
npm WARN deprecated fsevents@1.2.12: fsevents 1 will break on node v14+. Upgrade to fsevents 2 with massive improvements.
npm WARN deprecated browserslist@1.7.7: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.

> fsevents@1.2.12 install /Users/l/Desktop/VueTemp/vueDemo/vuedemo001/node_modules/fsevents
> node-gyp rebuild

  SOLINK_MODULE(target) Release/.node
  CXX(target) Release/obj.target/fse/fsevents.o
  SOLINK_MODULE(target) Release/fse.node

> core-js@2.6.11 postinstall /Users/l/Desktop/VueTemp/vueDemo/vuedemo001/node_modules/core-js
> node -e "try{require('./postinstall')}catch(e){}"

Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!

The project needs your help! Please consider supporting of core-js on Open Collective or Patreon:
> https://opencollective.com/core-js
> https://www.patreon.com/zloirock

Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)


> ejs@2.7.4 postinstall /Users/l/Desktop/VueTemp/vueDemo/vuedemo001/node_modules/ejs
> node ./postinstall.js

Thank you for installing EJS: built with the Jake JavaScript build tool (https://jakejs.com/)


> uglifyjs-webpack-plugin@0.4.6 postinstall /Users/l/Desktop/VueTemp/vueDemo/vuedemo001/node_modules/webpack/node_modules/uglifyjs-webpack-plugin
> node lib/post_install.js

npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN ajv-keywords@3.4.1 requires a peer of ajv@^6.9.1 but none is installed. You must install peer dependencies yourself.

added 1304 packages from 688 contributors and audited 12074 packages in 73.643s

27 packages are looking for funding
  run `npm fund` for details

found 13 vulnerabilities (1 low, 8 moderate, 4 high)
  run `npm audit fix` to fix them, or `npm audit` for details

# Project initialization finished!
# ========================

To get started:

  cd vuedemo001
  npm run dev

Documentation can be found at https://vuejs-templates.github.io/webpack


 l@ls-MacBook-Air  ~/Desktop/VueTemp/vueDemo  cd vuedemo001
 l@ls-MacBook-Air  ~/Desktop/VueTemp/vueDemo/vuedemo001  npm run dev

> vuedemo001@1.0.0 dev /Users/l/Desktop/VueTemp/vueDemo/vuedemo001
> webpack-dev-server --inline --progress --config build/webpack.dev.conf.js

 12% building modules 21/29 modules 8 active ...ueTemp/vueDemo/vuedemo001/src/App.vue{ parser: "babylon" } is deprecated; we now treat it as { parser: "babel" }.
 95% emitting

 DONE  Compiled successfully in 8110ms                                                           3:26:40 PM

 I  Your application is running here: http://localhost:8080


 WAIT  Compiling...                                                                              3:27:53 PM

 95% emitting

 DONE  Compiled successfully in 1213ms                                                           3:27:55 PM

 I  Your application is running here: http://localhost:8080

```

