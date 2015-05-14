# springCloudConfig
git repository serving properties for spring-cloud config

## cloud-config server
A spring cloud-config server would look like

```
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {
   public static void main(String[] args) {
      SpringApplication.run(ConfigServerApplication.class, args);
   }
}
```

By accessing ``http://<configServer>:8888/{name}/{env}/{label}``, you can get the configuration for each environment(profile) of each application.

Probably you can regard  
- ``name`` as application name
- ``env`` as profile name (default is ``default``)
- ``label`` as branch name (default is ``master``)

label can be omitted.

## cloud-config client
A spring cloud-config client needs to have it's application name and the uri of this git repo in its ``bootstrap.yml`` on the classpath.  
Remember, it is NOT ``application.yml``, because the config has to be read *before* the spring IoC Container with all its beans is initialized!

```
spring:
  application:
    name: configClient
  cloud:
    config:
      uri: https://github.com/dhoffi/springCloudConfig.git
      failFast: false # if true fail (exit) if the config server is not reached on startup
```

for more information: [good blog post](http://qiita.com/making@github/items/704d8e254e03c5cce546 Dynamic configuration management with Spring Cloud Config)

