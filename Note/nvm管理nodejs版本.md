[使用nvm管理node多版本（安装、卸载nvm，配置环境变量） - 与f - 博客园](https://www.cnblogs.com/fps2tao/p/18198038)





nvm list available   查询可下载版本号





安装指定node.js版本 ：  nvm install 16.14.0



安装完成后开始插入nodejs首先使用 nvm list available 查询可插入版本号，LST表示可插入稳定版本。【如未指定版本，建议安装LTS下的版本】



nvm use 切换node版本。(如果报错，用管理员身份打开重新 nvm use 你指定的版本） ：nvm use 16.14.0



安装完成后可以分别输入命令行 node -v 和 npm -v，检验node.js以及对应npm是否安装成功



nvm list 查看当前已安装的node.js版本，带*号的是正在使用的