# Builder webpack ![Travis](https://app.travis-ci.com/TaylorDurden/builder-webpack.svg?branch=main)

![功能模块设计](http://rf0q9h2rh.hn-bkt.clouddn.com/webpack-general-design.PNG)

## node -v => 10.15.3

# 编写可维护的webpack构建配置
-------------
## 构建配置抽离成npm包的意义

### 通用性
  - 业务开发者无需关注构建配置
  - 统一团队构建脚本

### 可维护性
  - 构建配置合理的拆分
  - README文档、ChangeLog文档等

### 质量
  - 冒烟测试、单元测试、测试覆盖率
  - 持续集成
-------------
## 构建配置管理的可选方案

通过多个配置文件管理不同环境的构建，webpack --config 参数进行控制

将构建配置设计成一个库，比如：hjs-webpack、Neutrino、webpack-blocks

抽成一个工具进行管理，比如: create-react-app, kyt, nwb

将所有的配置放在一个文件，通过 --env 参数控制分支选择

-------------
## 构建配置包设计

### 通过多个配置文件管理不同环境的 webpack 配置：
  - 基础配置：webpack.base.js
  - 开发环境：webpack.dev.js
  - 生产环境：webpack.prod.js
  - SSR环境：webpack.ssr.js

### 抽离成一个 npm 包统一管理
  - 规范：Git commit日志、README、ESLint规范、Semver规范
  - 质量：冒烟测试、单元测试、测试覆盖率和CI
-------------
## 通过 webpack-merge 组合配置

```bash
> merge = require("webpack-merge")
...
> merge (
...{ a: [1], b: 5, c: 20},
...{ a: [2], b: 10, c: 421},
...)
{ a: [1, 2], b: 10, c: 20, d: 421 }
```

合并配置：module.exports = merge(baseConfig, devConfig);

