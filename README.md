# nest-microservices-logger
- A NestJS module to handle customized logging for `generator-nest-microservices` yeoman template
### How to use
- install package with `npm i -S nest-microservices-logger`
- Register the `LoggerModule` to your feature modules:
```
@Module({})
export class AppModule {
  static register(config: ConfigOptions): DynamicModule {
    return {
      module: AppModule,
      imports: [
        LoggerModule.register({ appName: 'my-app-name' }),
        ...
      ],
    };
  }
}
```
- Once `LoggerModule` is registered, then you can inject the `LoggerService` to your providers and use available `log`, `warn` or `error` functions:
```
export class ExampleController {
  constructor (private logger: LoggerService) {}
  logSomething() {
    this.logger.log('it works!');
  }
}
```
### Logger options
|Property|Type|Required|Description|
|-|-|-|-|
|file|`FileTransportOptions`|false|Winston's file transport options object. More info can be found here https://github.com/winstonjs/winston/blob/master/docs/transports.md#file-transport%7C
|elasticSearch|`ESTransportOptions`|false| contains `{ url, index }` to be used for Elastic Search logging
|console|`ConsoleTransportOptions`|false|Winston's console transport options object. More info can be found here https://github.com/winstonjs/winston/blob/master/docs/transports.md#console-transport%7C
|appName|`String`|true|This is logger's context name|