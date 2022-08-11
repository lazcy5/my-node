##### Nest.js 安装

```bash
# 全局安装
npm i -g @nestjs/cli
# 创建项目
nest new project-name 
```

##### Nest-cli 命令

```bash
nest g [文件类型] [文件名] [文件目录]

# 创建模块
nest g mo posts
# 创建控制器
nest g co posts   nest g co article
# 创建服务类
nest g service posts   nest g service article

# 注意创建顺序：先创建Module,再创建Controller和Service，这样创建出来的文件在Module中自动注册，反之，后创建Module，Controller和Service会被注册到外层的app.modle.ts
```

