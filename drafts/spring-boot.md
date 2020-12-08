# Spring Boot

Spring Initalizr
https://start.spring.io

spring --version
brew install 

spring init --dependencies=CSV projectName 

spring run app.groovy    // Uses TomCat


@SpringBootApplication // shortcut annotation

https://docs.spring.io/spring-boot/docs/



MVC
Add dependency: spring-boot-starter-web 

Spring Boot annotations:
@Controller // class level
@GetMapping("/path"). // can return model

Spring MVC anotations:

@RestController // class level. -- @Controller @ResponseBody
@RequestMapping ("/path") // class level
@GetMapping("/path/{arg}") // returns ResponseEntity<>
@PathVariable("arg") // variable level


ResponseStatusException

Another delendency: spring-boot-starter-thymeleaf


Plugins: spring-boot-maven-plugin

dependency: spring-boot-starter-actuator
/actuator
/actuator/health




@Scheduled(cron="${synctask.cron}")




Exception handling (e.g. in a controller)
 @ExceptionHandler({ Throwable.class })
    protected void handleInvalidRequest(Throwable t) throws Throwable {
        log.error(t.getMessage());
        throw t;
    }

