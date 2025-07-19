# Rule: Generating a Task List from a PRD (Spring Boot Edition)
## Goal
To guide an AI assistant in creating a detailed, step-by-step task list in Markdown format based on an existing Product Requirements Document (PRD). The task list should guide a developer through Spring Boot implementation using package-by-functionality structure.

## Output
- **Format:** Markdown (`.md`)
- **Location:** `/tasks/`
- **Filename:** `tasks-[prd-file-name].md` (e.g., `tasks-prd-user-profile-editing.md`)

## Process
1.  **Receive PRD Reference:** The user points the AI to a specific PRD file
2.  **Analyze PRD:** The AI reads and analyzes the functional requirements, user stories, and other sections of the specified PRD.
3.  **Phase 1: Generate Parent Tasks:** Based on the PRD analysis, create the file and generate the main, high-level tasks required to implement the feature. Use your judgement on how many high-level tasks to use. It's likely to be about 5-7 for Spring Boot projects. Present these tasks to the user in the specified format (without sub-tasks yet). Inform the user: "I have generated the high-level tasks based on the PRD. Ready to generate the sub-tasks? Respond with 'Go' to proceed."
4.  **Wait for Confirmation:** Pause and wait for the user to respond with "Go".
5.  **Phase 2: Generate Sub-Tasks:** Once the user confirms, break down each parent task into smaller, actionable sub-tasks necessary to complete the parent task. Ensure sub-tasks logically follow from the parent task and cover the Spring Boot implementation details implied by the PRD.
6.  **Identify Relevant Files:** Based on the tasks and PRD, identify potential files that will need to be created or modified using package-by-functionality structure. List these under the `Relevant Files` section, including corresponding test files if applicable.
7.  **Generate Final Output:** Combine the parent tasks, sub-tasks, relevant files, and notes into the final Markdown structure.
8.  **Save Task List:** Save the generated document in the `/tasks/` directory with the filename `tasks-[prd-file-name].md`, where `[prd-file-name]` matches the base name of the input PRD file (e.g., if the input was `prd-user-profile-editing.md`, the output is `tasks-prd-user-profile-editing.md`).

## Spring Boot Package Structure Guidelines
When identifying files and organizing tasks, follow **package-by-functionality** approach:

### Package Structure Example:
```
src/main/java/com/company/app/
├── userprofile/
│   ├── UserProfileController.java
│   ├── UserProfileService.java
│   ├── UserProfileRepository.java
│   ├── UserProfile.java (entity)
│   ├── UserProfileDto.java
│   └── UserProfileMapper.java
├── payment/
│   ├── PaymentController.java
│   ├── PaymentService.java
│   ├── PaymentRepository.java
│   └── Payment.java (entity)
├── config/
│   ├── DatabaseConfig.java
│   ├── SecurityConfig.java
│   └── ApplicationProperties.java
├── common/
│   ├── exception/
│   │   ├── GlobalExceptionHandler.java
│   │   └── CustomExceptions.java
│   ├── response/
│   │   ├── ApiResponse.java
│   │   └── ErrorResponse.java
│   └── constants/
│       └── MessageConstants.java
└── Application.java
```

### Resource Structure:
```
src/main/resources/
├── application.yml
├── application-dev.yml
├── application-test.yml
├── application-prod.yml
└── db/migration/
    ├── V1__Create_user_profile_table.sql
    └── V2__Add_payment_tables.sql
```

## Output Format
The generated task list *must* follow this structure:

```markdown
## Relevant Files

### Main Application Files
- `src/main/java/com/company/app/[feature]/[Feature]Controller.java` - REST controller for [feature] endpoints
- `src/main/java/com/company/app/[feature]/[Feature]Service.java` - Business logic for [feature] operations
- `src/main/java/com/company/app/[feature]/[Feature]Repository.java` - Data access layer for [feature] entities
- `src/main/java/com/company/app/[feature]/[Feature].java` - JPA entity for [feature]
- `src/main/java/com/company/app/[feature]/[Feature]Dto.java` - Data transfer object for [feature] API
- `src/main/java/com/company/app/[feature]/[Feature]Mapper.java` - Entity to DTO mapping logic

### Configuration Files
- `src/main/java/com/company/app/config/[Feature]Config.java` - Configuration class for [feature]-specific beans
- `src/main/resources/application.yml` - Main application configuration
- `src/main/resources/application-test.yml` - Test-specific configuration

### Database Migration
- `src/main/resources/db/migration/V[X]__[description].sql` - Flyway migration for database schema

### Common/Shared Files
- `src/main/java/com/company/app/common/exception/GlobalExceptionHandler.java` - Global exception handling
- `src/main/java/com/company/app/common/response/ApiResponse.java` - Standardized API response wrapper
- `src/main/java/com/company/app/common/constants/MessageConstants.java` - Externalized message constants

### Test Files
- `src/test/java/com/company/app/[feature]/[Feature]ControllerTest.java` - Unit tests for controller layer
- `src/test/java/com/company/app/[feature]/[Feature]ServiceTest.java` - Unit tests for service layer
- `src/test/java/com/company/app/[feature]/[Feature]RepositoryTest.java` - Repository integration tests
- `src/test/java/com/company/app/[feature]/[Feature]IntegrationTest.java` - Full integration tests
- `src/test/resources/application-test.yml` - Test configuration properties

### Notes
- **Package Organization**: Use package-by-functionality (not by layer). Each feature gets its own package containing all its layers.
- **Test Placement**: Test files mirror the main source structure under `src/test/java/`
- **Configuration**: Use `@ConfigurationProperties` classes for type-safe configuration
- **Database**: Use Flyway migrations for all schema changes
- **Testing Strategy**: 
  - Unit tests for service logic with `@ExtendWith(MockitoExtension.class)`
  - Integration tests for repositories with `@DataJpaTest`
  - Web layer tests with `@WebMvcTest`
  - Full application tests with `@SpringBootTest`
- **Test Execution**: Use `mvn clean verify` to run all tests including integration tests
- **Naming Convention**: Use conventional Spring Boot naming (Controller, Service, Repository suffixes)

## Tasks
- [ ] 1.0 Database Schema and Migration Setup
  - [ ] 1.1 [Create Flyway migration scripts for required tables]
  - [ ] 1.2 [Create JPA entities with proper annotations]
- [ ] 2.0 Core Business Logic Implementation  
  - [ ] 2.1 [Implement service layer with business rules]
  - [ ] 2.2 [Create repository interfaces with custom queries if needed]
- [ ] 3.0 API Layer Development
  - [ ] 3.1 [Implement REST controllers with proper endpoints]
  - [ ] 3.2 [Create DTOs and request/response models]
  - [ ] 3.3 [Implement entity-DTO mapping logic]
- [ ] 4.0 Configuration and Exception Handling
  - [ ] 4.1 [Create configuration classes with @ConfigurationProperties]
  - [ ] 4.2 [Implement global exception handler with @ControllerAdvice]
  - [ ] 4.3 [Create standardized API response wrappers]
- [ ] 5.0 Testing Implementation
  - [ ] 5.1 [Write unit tests for service layer]
  - [ ] 5.2 [Write integration tests for repository layer]
  - [ ] 5.3 [Write web layer tests for controllers]
  - [ ] 5.4 [Write end-to-end integration tests]
- [ ] 6.0 Documentation and Monitoring
  - [ ] 6.1 [Add OpenAPI documentation with Springdoc]
  - [ ] 6.2 [Configure Actuator endpoints for monitoring]
  - [ ] 6.3 [Add structured logging with correlation IDs]
```

## Spring Boot Specific Task Categories
When generating tasks, consider these Spring Boot-specific categories:

1. **Database and Persistence**
   - Flyway migrations
   - JPA entities and relationships
   - Custom repository methods
   - Database configuration

2. **Business Logic and Services**
   - Service layer implementation
   - Transaction management
   - Validation logic
   - Business rule enforcement

3. **API and Web Layer**
   - REST controller endpoints
   - Request/response DTOs
   - Input validation
   - API documentation

4. **Configuration Management**
   - Application properties
   - Profile-specific configurations
   - Bean configuration classes
   - Security configuration

5. **Testing Strategy**
   - Unit tests (service layer)
   - Integration tests (repository layer)
   - Web layer tests (controller layer)
   - End-to-end tests (full application)

6. **Cross-Cutting Concerns**
   - Exception handling
   - Logging and monitoring
   - Security implementation
   - Performance considerations

## Interaction Model
The process explicitly requires a pause after generating parent tasks to get user confirmation ("Go") before proceeding to generate the detailed sub-tasks. This ensures the high-level plan aligns with user expectations before diving into Spring Boot implementation details.

## Target Audience
Assume the primary reader of the task list is a **junior Spring Boot developer** who will implement the feature using modern Spring Boot practices and package-by-functionality organization.
