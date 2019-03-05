# 小程序使用说明

## 软件安装

安装腾讯小程序开发环境。
https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html


安装node。
https://nodejs.org/en/


## 系统说明

使用的主要组件是mpvue和echarts 。 如果node_modules目录下的文件缺失了，请自行npm安装 。


## 使用方法

开发和在模拟器(腾讯小程序开发环境)调试：在所在目录命令行环境下运行npm run dev，成功后即可进入开发环境，对目录下文件的修改保存后，会被自动编译到小程序的开发环境中，实时生效。


发布：在所在目录命令行环境下运行npm run build，成功后即可在小程序的开发运行环境中点击预览或者发布按钮，可以在手机上真机测试或者发布到小程序的后台，登录微信公众平台后即可提交审核发布。

## 目录说明

build/   webpack配置和build配置(如果没有引入新的组件，一般不用修改)

config/ npm run 的配置(一般不用修改)

dist/   编译输出目录

node_modules/  node的库目录

src/pages/  页面目录(修改页面在这个目录内)

src/components/  页面组件目录(修改组件在这个目录内)

src/utils/  中间件目录(修改和服务器对接数据的处理在api.js文件中)

src/pages.js  加入新的页面需要在这个文件注册

static/ 静态资源(图片)所在目录