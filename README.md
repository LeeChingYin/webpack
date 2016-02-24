# webpack
Webpack 简单项目

跟着教程边学边打代码，建立项目（教程地址http://zhuanlan.zhihu.com/FrontendMagazine/20367175）
按着教程写完index.js,sub.js,配置好webpack后，然后在项目根目录运行webpack后，马上遇到一个坑
moudule.js:338
      throw err;
Error: Cannot find module 'webpack/lib/node/NodeTemplatePlugin'

指令webpack安装的时候明明是全局的 “npm install -g webpack”，但是仍然报出了这样的错误
根据路径，ls查看webpack目录下是存在NodeTemplatePlugin这个插件的，查找了一下原因，应该是没有设置环境变量导致的。https://segmentfault.com/a/1190000002478924
按照别人的方法：
  1.直接在终端下，设置环境变量export NODE_PATH="/usr/local/lib/node_modules" 后在项目根目录运行webpack，仍然报错。在项目根目录下输入指令 echo $NODE_PATH 输出结果为空。
  2.在项目根目录下设置环境变量export NODE_PATH="/usr/local/lib/node_modules" 后在项目根目录运行webpack，成功！在项目根目录下输入指令 echo $NODE_PATH 能输出结果。但是当新开一个终端进入项目，并在项目根目录下运行webpack指令，仍然报错，输入指令 echo $NODE_PATH 输出结果为空。说明之前设置的环境变量只是一个临时的值！
  以上两种方法都不可以很好的解决问题。
  
继续寻找解决方案：
在~/.bash_profile中添加如下设置：
  export NODE_PATH="/usr/local/lib/node_modules"
  保存退出。
  
  运行webpack,成功！输入指令 echo $NODE_PATH 能输出结果！
  
  ps：在终端下 vim ~/.bash_profile
      i  #进入编辑
      输入语句 export NODE_PATH="/usr/local/lib/node_modules"
      esc
      :wq
      source ~/.bash_profile
      让~/.bash_profile马上生效！
