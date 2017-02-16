https://app.pluralsight.com/player?course=spring-boot-efficient-development-configuration-deployment&author=dustin-schultz&name=spring-boot-efficient-development-configuration-deployment-m0&clip=0&mode=live


# Leveraging Initializr and Devtools for Efficient Development
Spring initializer

*Tip* F1 to show documentation

`@Value("{server.port}")` - to read config values

## How to run in IDEA
Add to dependencies: Spring boot dev tools

For fast-rebooting in IDEA record macro to restart application and bing it to shortcut:
Go to macros -> start recording.
Press File -> save all. 
Press Build -> Build project.
Go to macros -> stop recorging. 
Name macros and go to key bindings -> macros to add shortcut.

Spring-dev-tools should reload only changed files. For more reference:
http://docs.spring.io/spring-boot/docs/current/reference/html/using-boot-devtools.html#using-boot-devtools-restart

And according to logs:
First run:
```
...Root WebApplicationContext: initialization completed in 2974 ms
```
Reload run:
```
...Root WebApplicationContext: initialization completed in 611 ms
```

# Reducing Code with Custom Auto Configurations

## Configuration
```
@Configuration
@ComponentScan
@EnableAutoConfiguration
```
is the same as 
```
@SpringBootApplication
```

Conditions for configuration:
 - presense/absence of Jar.
 - presense/absence of beans
 - presence/absence of property
 
