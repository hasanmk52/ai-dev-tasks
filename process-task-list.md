# Task List Management
Guidelines for managing task lists in markdown files to track progress on completing a PRD

## Task Implementation
- **One sub-task at a time:** Do **NOT** start the next sub‑task until you ask the user for permission and they say "yes" or "y"
- **Completion protocol:**  
  1. When you finish a **sub‑task**, immediately mark it as completed by changing `[ ]` to `[x]`.
  2. If **all** subtasks underneath a parent task are now `[x]`, follow this sequence:
    - **First**: Run the full test suite based on project type:
      - **Spring Boot/Maven**: `mvn clean verify` (runs unit tests, integration tests, and static analysis)
      - **Spring Boot/Gradle**: `./gradlew clean build` or `./gradlew clean test integrationTest`
      - **Node.js**: `npm test` or `npm run test:coverage`
      - **Python**: `pytest` or `python -m pytest --cov`
      - **Ruby**: `bin/rails test` or `bundle exec rspec`
      - **General**: Run project-specific test command
    - **Only if all tests pass**: Stage changes (`git add .`)
    - **Clean up**: Remove any temporary files and temporary code before committing
    - **Commit**: Use a descriptive commit message that:
      - **First**: Ask for the Jira task ID if applicable (e.g., "CAM-192", "PROJ-456")
      - Uses conventional commit format (`feat:`, `fix:`, `refactor:`, etc.)
      - Summarizes what was accomplished in the parent task
      - Lists key changes and additions
      - References the task number and PRD context
      - **Formats the message as a single-line command using `-m` flags**, e.g.:
        ```
        git commit -m "CAM-192: feat: add payment validation logic" -m "- Validates card type and expiry" -m "- Adds unit tests for edge cases" -m "Related to T123 in PRD"
        ```
  3. Once all the subtasks are marked completed and changes have been committed, mark the **parent task** as completed.
- Stop after each sub‑task and wait for the user's go‑ahead.

## Task List Maintenance
1. **Update the task list as you work:**
   - Mark tasks and subtasks as completed (`[x]`) per the protocol above.
   - Add new tasks as they emerge.
2. **Maintain the "Relevant Files" section:**
   - List every file created or modified.
   - Give each file a one‑line description of its purpose.

# AI Instructions
## When working with task lists, the AI must:
1. Regularly update the task list file after finishing any significant work.
2. Follow the completion protocol:
   - Mark each finished **sub‑task** `[x]`.
   - Mark the **parent task** `[x]` once **all** its subtasks are `[x]`.
3. Add newly discovered tasks.
4. Keep "Relevant Files" accurate and up to date.
5. Before starting work, check which sub‑task is next.
6. After implementing a sub‑task, update the file and then pause for user approval.

## 🏗️ ENGINEERING STANDARDS
**Code Quality Requirements:**
1. **No Hardcoded Values**
   - ❌ NEVER hardcode IPs, ports, timeouts
   - ✅ Use configuration files, environment variables, or constants
   - ✅ Spring Boot: Use `@ConfigurationProperties` and `application.yml/properties`
2. **Externalized Text**
   - ❌ NEVER hardcode user-facing messages in code
   - ✅ Use message catalogs or constants files
   - ✅ Spring Boot: Use constants or enums for error messages and responses
3. **Consistent Response Format**
   - ✅ Always use success/error response wrappers
   - ✅ Standardized error codes and messages
   - ✅ Spring Boot: Use `@ControllerAdvice` for global exception handling
   - ✅ Consistent API response structure with `ResponseEntity<T>`
4. **Comprehensive Testing**
   - ✅ Unit tests for ALL business logic (minimum 80% coverage)
   - ✅ Spring Boot: Use `@ExtendWith(MockitoExtension.class)` for unit tests
   - ✅ Integration tests for API endpoints
   - ✅ Spring Boot: Use `@SpringBootTest` for full context integration tests
   - ✅ Spring Boot: Use `@WebMvcTest` for web layer testing with MockMvc
   - ✅ Spring Boot: Use `@DataJpaTest` for repository layer testing
   - ✅ Performance tests for critical paths
   - ✅ Security tests for authentication/authorization
   - ✅ Spring Boot: Use `@WithMockUser` for security testing
5. **Production-Ready Code**
   - ✅ Proper error handling and recovery
   - ✅ Structured logging with correlation IDs
   - ✅ Spring Boot: Use SLF4J with Logback and MDC for correlation
   - ✅ Metrics and monitoring hooks
   - ✅ Spring Boot: Use Micrometer and Actuator endpoints
   - ✅ Graceful degradation patterns
   - ✅ Circuit breakers for external services
   - ✅ Spring Boot: Use Resilience4j for circuit breakers and retry logic

**Spring Boot Specific Standards:**
6. **Configuration Management**
   - ✅ Use `@ConfigurationProperties` for type-safe configuration
   - ✅ Separate profiles for different environments (`dev`, `test`, `prod`)
   - ✅ Use `@Validated` on configuration classes
7. **Dependency Injection**
   - ✅ Use constructor injection (required dependencies)
   - ✅ Avoid `@Autowired` on fields (use constructor or setter injection)
   - ✅ Use `@RequiredArgsConstructor` from Lombok when appropriate
8. **Database Integration**
   - ✅ Use Spring Data JPA with proper entity mapping
   - ✅ Implement custom repositories when needed
   - ✅ Use Flyway for database migrations
9. **API Documentation**
   - ✅ Use OpenAPI 3 (Springdoc) for API documentation
   - ✅ Document all endpoints with proper examples

**Testing Implementation Checklist:**
- [ ] **Unit Tests**: Test business logic in isolation
  - [ ] Service layer tests with mocked dependencies
  - [ ] Utility/helper class tests
  - [ ] Custom validator tests
- [ ] **Integration Tests**: Test component interactions
  - [ ] Repository tests with `@DataJpaTest`
  - [ ] Web layer tests with `@WebMvcTest`
  - [ ] Full application tests with `@SpringBootTest`
- [ ] **End-to-End Tests**: Test complete user workflows
  - [ ] API endpoint tests with real HTTP calls
  - [ ] Database integration tests
- [ ] **Test Configuration**
  - [ ] Separate `application-test.properties` for test configuration
  - [ ] Test containers for database testing (if needed)
  - [ ] Mock external services appropriately

**Implementation Checklist:**
- [ ] Remove ALL hardcoded values
- [ ] Create `@ConfigurationProperties` classes
- [ ] Implement `@ControllerAdvice` for error handling
- [ ] Add comprehensive unit tests (`@ExtendWith(MockitoExtension.class)`)
- [ ] Add integration tests (`@SpringBootTest`, `@WebMvcTest`, `@DataJpaTest`)
- [ ] Externalize all messages to constants or enums
- [ ] Add structured logging with SLF4J
- [ ] Implement proper exception handling
- [ ] Add Actuator endpoints for monitoring
- [ ] Configure profiles for different environments
- [ ] Run `mvn clean verify` to ensure all tests pass
