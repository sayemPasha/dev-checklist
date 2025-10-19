# .NET Development Checklist

## Architecture & Design
- [ ] **Architectural Patterns**
  - [ ] Clean Architecture / Onion Architecture
  - [ ] CQRS (with MediatR)
  - [ ] Domain-Driven Design (DDD) fundamentals
- [ ] **Dependency Injection**
  - [ ] Built-in .NET DI container or 3rd-party (Autofac, Lamar)
  - [ ] Scoped, Transient, Singleton lifetimes used correctly
- [ ] **Layered Structure**
  - [ ] Separation of concerns: Presentation, Application, Domain, Infrastructure
  - [ ] Repository + Unit of Work pattern
  - [ ] Single Source of Truth for data
- [ ] **API Design (for backend)**
  - [ ] RESTful conventions (or gRPC / GraphQL if applicable)
  - [ ] Versioning strategy (URL, header, or query param)
  - [ ] OpenAPI/Swagger documentation
- [ ] **Cross-Cutting Concerns**
  - [ ] Middleware pipeline (logging, auth, error handling)
  - [ ] Centralized exception handling
  - [ ] Health checks (`Microsoft.Extensions.Diagnostics.HealthChecks`)

## Concurrency & Background Work
- [ ] **Async/Await**
  - [ ] Proper `async`/`await` usage (avoid `.Result` or `.Wait()`)
  - [ ] `ConfigureAwait(false)` in libraries
- [ ] **Background Services**
  - [ ] `IHostedService` / `BackgroundService`
  - [ ] Hangfire, Quartz.NET, or Azure Functions for scheduled work
  - [ ] Message queues (RabbitMQ, Azure Service Bus, Kafka)
- [ ] **Threading & Synchronization**
  - [ ] Thread-safe collections (`ConcurrentQueue`, `Channel<T>`)
  - [ ] Avoid deadlocks with async code
  - [ ] Use `CancellationToken` for cancellable operations

## Networking & APIs
- [ ] **HTTP Clients**
  - [ ] `HttpClient` with `IHttpClientFactory` (avoid client reuse anti-pattern)
  - [ ] Polly for resilience (retry, circuit breaker)
- [ ] **API Consumption**
  - [ ] Typed clients
  - [ ] Serialization with `System.Text.Json` (or Newtonsoft.Json if needed)
- [ ] **Real-Time Communication**
  - [ ] SignalR for WebSockets / real-time updates
  - [ ] Azure SignalR Service (for scale)
- [ ] **Security**
  - [ ] HTTPS enforcement
  - [ ] Certificate pinning (if required, via `HttpClientHandler`)
  - [ ] Secure headers (CSP, HSTS, etc.)
- [ ] **Caching**
  - [ ] In-memory (`IMemoryCache`)
  - [ ] Distributed caching (Redis, SQL Server)
  - [ ] HTTP response caching (`[ResponseCache]`)

## Persistence & Databases
- [ ] **ORM / Data Access**
  - [ ] Entity Framework Core (Code-First preferred)
  - [ ] Dapper for performance-critical scenarios
  - [ ] Raw SQL only when necessary (with parameterization)
- [ ] **Database Strategies**
  - [ ] Migrations (`dotnet ef migrations`)
  - [ ] Seeding strategies
- [ ] **Connection Resilience**
  - [ ] Retry logic for transient failures
  - [ ] Connection pooling configured

## Security & Authentication
- [ ] **Authentication**
  - [ ] JWT Bearer tokens (ASP.NET Core Identity + JWT)
  - [ ] OAuth 2.0 / OpenID Connect (with IdentityServer or Azure AD)
  - [ ] Cookie-based auth for web apps
- [ ] **Authorization**
  - [ ] Policy-based authorization
  - [ ] Role & claim-based checks
  - [ ] Resource-based authorization
- [ ] **Data Protection**
  - [ ] ASP.NET Core Data Protection API
  - [ ] AES encryption for sensitive local data (e.g., biometric-protected keys)
  - [ ] Secure storage on device (MAUI: `SecureStorage`)
- [ ] **Biometrics (Mobile/Desktop)**
  - [ ] MAUI Essentials: `BiometricAuthentication`
  - [ ] Windows Hello / Face ID / Touch ID integration


## Performance & Optimization
- [ ] **Profiling & Monitoring**
  - [ ] Application Insights (Azure) or OpenTelemetry
  - [ ] Memory/CPU profiling (Visual Studio Profiler, dotTrace)
- [ ] **Optimizations**
  - [ ] Lazy loading disabled in EF Core (explicit loading preferred)
  - [ ] Compiled models (EF Core 6+)
  - [ ] Minimal APIs for lightweight endpoints
- [ ] **Client-Side (MAUI/Web)**
  - [ ] Image caching & compression (FFImageLoading, SkiaSharp)
  - [ ] Virtualized lists (`CollectionView`)
  - [ ] Ahead-of-Time (AOT) compilation (for MAUI on iOS/Android)
- [ ] **Startup Performance**
  - [ ] Trimmed deployments (`.NET trim`)
  - [ ] ReadyToRun compilation

## Testing & Automation
- [ ] **Unit Testing**
  - [ ] xUnit / NUnit / MSTest
  - [ ] Moq / NSubstitute for mocking
  - [ ] Testable architecture (no statics, inject dependencies)
- [ ] **Integration Testing**
  - [ ] `WebApplicationFactory` for ASP.NET Core
  - [ ] Testcontainers for DB integration tests
- [ ] **UI Testing**
  - [ ] Appium / Xamarin.UITest for MAUI
  - [ ] Playwright / Selenium for web
- [ ] **CI/CD**
  - [ ] GitHub Actions / Azure DevOps / GitLab CI
  - [ ] Automated test runs, code coverage (Coverlet)
  - [ ] SonarQube / CodeQL for static analysis

## Release & Distribution
- [ ] **Packaging**
  - [ ] Single-file publish (`dotnet publish -p:PublishSingleFile=true`)
  - [ ] Self-contained vs framework-dependent
- [ ] **Obfuscation & Protection**
  - [ ] ConfuserEx / Dotfuscator (for desktop/mobile)
  - [ ] Code signing (Authenticode, Apple/Google signing)
- [ ] **Deployment**
  - [ ] Azure App Service / AWS Elastic Beanstalk
  - [ ] Docker containers (multi-stage builds)
- [ ] **Monitoring in Production**
  - [ ] Logging (Serilog + Seq / Application Insights)
  - [ ] Alerting on errors/performance degradation

## Domain-Specific Expertise
- [ ] **FinTech**
  - [ ] PCI-DSS compliance
  - [ ] Payment gateways (Stripe, Adyen SDKs)
  - [ ] Idempotency in APIs
- [ ] **Social / Collaboration**
  - [ ] Real-time chat (SignalR + Redis backplane)
  - [ ] Media upload with resumable chunks + CDN
