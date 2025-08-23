2025-08-21 21:28
Status: #baby
Tags: [[java]]
## Main

In **Spring Framework**, annotations are metadata that provide configuration and behavior hints to the Spring container. They reduce or even eliminate the need for XML configuration.
Here’s a breakdown of the **common Spring annotations**:

## **Core Stereotype Annotations**

These mark classes for component scanning:

- `@Component` → Generic Spring-managed component.
- `@Service` → Specialized `@Component` for service layer.
- `@Repository` → Specialized `@Component` for DAO (Data Access Object) layer. Also enables exception translation.
- `@Controller` → Specialized `@Component` for Spring MVC controllers.
- `@RestController` → Combines `@Controller` + `@ResponseBody` (used for REST APIs).

## **Dependency Injection Annotations**

- `@Autowired` → Automatically injects dependencies by type.
- `@Qualifier("beanName")` → Resolves conflicts when multiple beans of the same type exist.
- `@Inject` (JSR-330) → Similar to `@Autowired`.
- `@Resource` (JSR-250) → Injection by name, then by type.

## **Configuration Annotations**

- `@Configuration` → Marks a class as a source of Spring bean definitions.
- `@Bean` → Declares a bean inside a `@Configuration` class.
- `@PropertySource("classpath:application.properties")` → Loads property files.
- `@Value("${property.name}")` → Injects values from properties.

## **Spring Boot Annotations**

- `@SpringBootApplication` → Combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`.
    
- `@EnableAutoConfiguration` → Auto-configures beans based on classpath and properties.
    
- `@ComponentScan` → Scans for beans in specified packages.

## **Spring MVC Annotations**
- `@RequestMapping("/path")` → Maps web requests to methods.
- `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping` → Shorthand for request mappings.
- `@PathVariable` → Extracts values from URI template.
- `@RequestParam` → Extracts query parameters.
- `@RequestBody` → Binds request body to method parameter.
- `@ResponseBody` → Returns object as JSON/XML instead of view.
- `@ModelAttribute` → Binds form data to model.

## **Testing Annotations**
- `@RunWith(SpringRunner.class)` → JUnit integration.
- `@SpringBootTest` → Loads full application context for integration tests.
- `@MockBean` → Creates a mock bean for testing.

**Transactional**
`@Transactional` → Transactions.
## References

https://www.digitalocean.com/community/tutorials/spring-annotations
https://www.techferry.com/articles/spring-annotations.html