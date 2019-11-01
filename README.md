
# 源码分析

## 文件结构

``` bash
/Users/liufang/openSource/FunnyLiu/egg-cluster
├── index.js - 暴露startCluster方法，使用lib/master.js的ready()
├── lib
|  ├── agent_worker.js
|  ├── app_worker.js
|  ├── master.js
|  └── utils
|     ├── manager.js
|     ├── messenger.js
|     ├── options.js
|     └── terminate.js

```

## 外部模块依赖

请在： http://npm.broofa.com?q=egg-cluster 查看

## 内部模块依赖

![img](./inner.svg)

## 逐个文件分析

### index.js

暴露startCluster方法，使用lib/master.js的ready()
  
### lib/master.js

### lib/utils/options.js

提供方法解析参数。

参数校验，大量使用原生assert模块来对参数进行校验。

### lib/utils/manager.js

提供类Manager，继承自EventEmitter。用于管理worker，提供一些列api。

### lib/utils/messenger.js



# egg-cluster

[![NPM version][npm-image]][npm-url]
[![build status][travis-image]][travis-url]
[![Test coverage][codecov-image]][codecov-url]
[![David deps][david-image]][david-url]
[![Known Vulnerabilities][snyk-image]][snyk-url]
[![npm download][download-image]][download-url]

[npm-image]: https://img.shields.io/npm/v/egg-cluster.svg?style=flat-square
[npm-url]: https://npmjs.org/package/egg-cluster
[travis-image]: https://img.shields.io/travis/eggjs/egg-cluster.svg?style=flat-square
[travis-url]: https://travis-ci.org/eggjs/egg-cluster
[codecov-image]: https://codecov.io/github/eggjs/egg-cluster/coverage.svg?branch=master
[codecov-url]: https://codecov.io/github/eggjs/egg-cluster?branch=master
[david-image]: https://img.shields.io/david/eggjs/egg-cluster.svg?style=flat-square
[david-url]: https://david-dm.org/eggjs/egg-cluster
[snyk-image]: https://snyk.io/test/npm/egg-cluster/badge.svg?style=flat-square
[snyk-url]: https://snyk.io/test/npm/egg-cluster
[download-image]: https://img.shields.io/npm/dm/egg-cluster.svg?style=flat-square
[download-url]: https://npmjs.org/package/egg-cluster

Cluster Manager for Egg

---

## Install

```bash
$ npm i egg-cluster --save
```

## Usage

```js
const startCluster = require('egg-cluster').startCluster;
startCluster({
  baseDir: '/path/to/app',
  framework: '/path/to/framework',
});
```

You can specify a callback that will be invoked when application has started. However, master process will exit when catch an error.

```js
startCluster(options, () => {
  console.log('started');
});
```

## Options

| Param        | Type      | Description                              |
| ------------ | --------- | ---------------------------------------- |
| baseDir      | `String`  | directory of application                 |
| framework    | `String`  | specify framework that can be absolute path or npm package |
| plugins      | `Object`  | plugins for unittest                     |
| workers      | `Number`  | numbers of app workers                   |
| sticky       | `Boolean` | sticky mode server                       |
| port         | `Number`  | port                                     |
| https        | `Object`  | start a https server, note: `key` / `cert` / `ca` should be full path to file |
| require      | `Array\|String` | will inject into worker/agent process |
| pidFile      | `String`  | will save master pid to this file |

## Env

EGG_APP_CLOSE_TIMEOUT: app worker boot timeout value

EGG_AGENT_CLOSE_TIMEOUT: agent worker boot timeout value

## License

[MIT](LICENSE)
