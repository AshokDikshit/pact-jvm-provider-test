# Pact JVM Provider Test

A Java-based provider verification project using Pact JVM framework to verify consumer-provider contracts.

## Overview

This project demonstrates how to implement provider-side contract testing using Pact JVM with JUnit 5. It verifies that the provider (ReqRes API) satisfies the contracts defined by consumers.

## Project Structure

```
pact-jvm-provider-test/
├── .github/
│   └── java-upgrade/
│       └── hooks/
│           └── scripts/
├── src/
│   └── test/
│       └── java/
│           └── org/
│               └── provider/
│                   └── verification/
│                       └── ContractVerificationTest.java
├── pom.xml
└── README.md
```

## Technologies Used

- **Java**: Programming language
- **Maven**: Build tool and dependency management
- **Pact JVM**: Contract testing framework
- **JUnit 5**: Testing framework
- **ReqRes API**: External API used as provider for testing

## Dependencies

- `au.com.dius.pact.provider:junit5` (v4.6.0) - Pact JVM provider testing with JUnit 5
- Maven Surefire Plugin (v3.1.2) - Test execution
- Pact Maven Plugin (v4.1.0) - Pact contract management

## Configuration

### Provider Configuration

- **Provider Name**: `ReqResInUsersAPI`
- **Target Host**: `reqres.in`
- **Protocol**: HTTPS
- **Port**: 443
- **Pact Directory**: `target/pacts/`
- **Pact Broker URL**: `http://localhost:9292/` (configurable)

### Maven Configuration

The project is configured with:
- Pact result publishing enabled
- Pact contracts loaded from `target/pacts` folder
- Support for Pact Broker integration
- Automated test execution with Maven Surefire

## Getting Started

### Prerequisites

- Java 8 or higher
- Maven 3.6 or higher
- Access to ReqRes API (https://reqres.in)

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd pact-jvm-provider-test
```

2. Install dependencies:
```bash
mvn clean install
```

### Running Tests

#### Run Provider Verification Tests

```bash
mvn test
```

#### Run with Pact Result Publishing

```bash
mvn test -Dpact.verifier.publishResults=true
```

#### Using Pact Maven Plugin

```bash
mvn au.com.dius.pact.provider:maven:verify
```

## Test Implementation

### ContractVerificationTest.java

The main test class that:
- Configures the provider as `ReqResInUsersAPI`
- Sets up HTTPS target pointing to `reqres.in:443`
- Loads Pact contracts from `target/pacts` folder
- Verifies each interaction defined in the contracts
- Supports state management for complex scenarios

### Key Features

1. **Provider Verification**: Automatically verifies all consumer contracts
2. **HTTPS Support**: Configured to test against HTTPS endpoints
3. **Flexible Contract Loading**: Supports both local files and Pact Broker
4. **State Management**: Ready for provider state setup (currently commented)
5. **Result Publishing**: Configurable publishing of verification results

## Pact Broker Integration

The project supports Pact Broker integration:

```java
@PactBroker(url = "http://localhost:9292"
    // ,authentication = @PactBrokerAuth(username = "pact_workshop", password = "pact_workshop")
)
```

**Note**: Pact Broker configuration is currently commented out. Uncomment and configure as needed.

## Provider States

Provider states can be implemented to set up specific conditions:

```java
@State({ "users api exist" })
public void allUsers() {
    // Setup code for this state
}
```

**Note**: State methods are currently commented out. Implement as needed for your contracts.

## Configuration Options

### System Properties

- `pact.verifier.publishResults`: Enable/disable publishing verification results
- `pact.skipPublish`: Skip publishing contracts (default: false)

### Maven Properties

- `pactDirectory`: Directory containing Pact files (default: `target/pacts/`)
- `pactBrokerUrl`: Pact Broker URL for contract retrieval
- `trimSnapshot`: Remove snapshot from version (default: false)

## Best Practices

1. **Contract Management**: Store contracts in version control or use Pact Broker
2. **State Management**: Implement provider states for complex scenarios
3. **CI/CD Integration**: Run verification tests in your build pipeline
4. **Result Publishing**: Publish results to Pact Broker for visibility
5. **Version Management**: Use meaningful versions for contract tracking

## Troubleshooting

### Common Issues

1. **Connection Issues**: Ensure the provider endpoint is accessible
2. **Contract Mismatches**: Check contract definitions match provider implementation
3. **Authentication**: Configure proper authentication for secured endpoints
4. **State Setup**: Implement required provider states for contract verification

### Debug Mode

Enable debug logging by adding to your test configuration:

```java
System.setProperty("pact.verifier.publishResults", "true");
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Resources

- [Pact JVM Documentation](https://docs.pact.io/implementation_guides/jvm)
- [JUnit 5 Documentation](https://junit.org/junit5/docs/current/user-guide/)
- [ReqRes API Documentation](https://reqres.in/)
- [Maven Documentation](https://maven.apache.org/guides/)

## Support

For questions or issues, please:
1. Check the documentation links above
2. Search existing issues in the repository
3. Create a new issue with detailed information
