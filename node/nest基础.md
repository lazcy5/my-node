##### 1 全局安装nest

```bash
$ npm i -g @nestjs/cli
```

##### 2 创建项目

```bash
$ nest new project-name
```

##### 3 运行程序

```bash
$ npm run start
# 监听代码变动
$ npm run start:watch

# 数据库连接依赖包
$ npm i sequelize sequelize-typescript mysql2 -S

# 密码加密依赖包
$ yarn add passport passport-jwt passport-local @nestjs/passport @nestjs/jwt -S

# 日志系统依赖包
$ yarn add log4js stacktrace-js -S

```

##### 4 设置全局前缀

```typescript
 /* main.ts */
// main文件中我们可以在项目监听前配置一个全局的api前缀
async function bootstrap() {
const app = await NestFactory.create(AppModule);
    //设置全局前缀
    app.setGlobalPrefix('api');
    await app.listen(3000);
  }
/* app.controller.ts */
@Controller('user') // 控制器设置路由前缀 我理解为局部路由
  export class AppController {
    constructor(private readonly appService: AppService) {}
    @Get('find') // 方法装饰器设置路由路径 这里我理解为设置api子路由
    getHello(): string {
      return this.appService.getHello();
        }
    }
```

- 以上方法在api中映射成完整的路由为 `GET api/user/find` 。

##### 5 创建文件

```bash
$ nest g [文件类型] [文件名] [文件目录（src目录下）]
# 创建controller
$ nest g controller user logical
# 创建module
$ nest g module user logical
# 创建service
$ nest g service user logical
# 中间件文件
$ nest g middleware logger middleware
# 拦截器文件
$ nest g interceptor transform interceptor
# 过滤器
$ nest g filter http-exception filter
# 其他错误捕获
$ nest g filter any-exception filter



nest g service commodity logical
nest g controller commodity logical
```

