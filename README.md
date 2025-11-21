# Multi-Agent Code Review System

## Overview

A comprehensive, multi-agent code review system built with Microsoft Semantic Kernel and C#, featuring specialized agents for different programming languages and seamless integration with Azure DevOps and Team Foundation Server through the Model Context Protocol (MCP).

## 🚀 Features

### Multi-Agent Architecture
- **Language-Specific Agents**: Dedicated review agents for C#, C++, and Python
- **Extensible Design**: Easy to add new language agents
- **Parallel Processing**: Concurrent code review execution for improved performance
- **Agent Orchestration**: Intelligent routing of files to appropriate agents

### Source Control Integration
- **Azure DevOps Support**: Full integration with Azure DevOps Services
- **Team Foundation Server**: Compatible with on-premises TFS installations
- **MCP Protocol**: Standardized communication through Model Context Protocol
- **Automated Workflows**: Pull request reviews with automated comment posting

### Advanced Code Analysis
- **Syntax Analysis**: Language-specific syntax and compilation error detection
- **Security Scanning**: Detection of common security vulnerabilities
- **Performance Analysis**: Identification of performance anti-patterns
- **Best Practices**: Enforcement of coding standards and conventions
- **Documentation Checks**: Validation of code documentation completeness

### Modern User Interface
- **WPF Application**: Modern, responsive Windows application
- **Real-time Progress**: Live progress tracking during reviews
- **Connection Management**: Intuitive source control connection setup
- **Results Export**: Export review results to JSON and CSV formats
- **Agent Configuration**: Per-agent settings and rule customization

## 🏗️ Architecture

### System Components

```
┌─────────────────────────────────────────────────────────────┐
│                      UI Layer (WPF)                        │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────┐  ┌─────────────────┐  ┌──────────────┐ │
│  │  MainWindow     │  │ ConnectionWindow │  │ SettingsWindow│ │
│  │  ViewModel      │  │    ViewModel    │  │   ViewModel   │ │
│  └─────────────────┘  └─────────────────┘  └──────────────┘ │
├─────────────────────────────────────────────────────────────┤
│                     Service Layer                          │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────┐  ┌─────────────────┐  ┌──────────────┐ │
│  │ Agent           │  │ MCP Service     │  │ Source Control│ │
│  │ Orchestrator    │  │                 │  │ Service       │ │
│  └─────────────────┘  └─────────────────┘  └──────────────┘ │
├─────────────────────────────────────────────────────────────┤
│                     Agent Layer                            │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────┐  ┌─────────────────┐  ┌──────────────┐ │
│  │ C# Agent        │  │ C++ Agent       │  │ Python Agent │ │
│  │ (Roslyn)        │  │ (Pattern-based) │  │ (AST-based)  │ │
│  └─────────────────┘  └─────────────────┘  └──────────────┘ │
├─────────────────────────────────────────────────────────────┤
│                     Core Layer                             │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────┐  ┌─────────────────┐  ┌──────────────┐ │
│  │ Models          │  │ Interfaces      │  │ Services     │ │
│  └─────────────────┘  └─────────────────┘  └──────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Agent Specialization

#### C# Agent (`CSharpCodeReviewAgent`)
- **Roslyn Integration**: Full C# syntax tree analysis
- **Naming Conventions**: PascalCase/camelCase enforcement
- **Complexity Analysis**: Cyclomatic complexity calculation
- **Security Checks**: SQL injection and hardcoded secret detection
- **Performance Analysis**: String concatenation and LINQ optimization
- **Documentation**: XML documentation validation

#### C++ Agent (`CppCodeReviewAgent`)
- **Memory Management**: Leak detection and smart pointer recommendations
- **Security Analysis**: Buffer overflow and unsafe function detection
- **Modern C++**: C++11/14/17/20 feature recommendations
- **Performance Optimization**: Container and algorithm efficiency
- **Best Practices**: RAII and const-correctness validation

#### Python Agent (`PythonCodeReviewAgent`)
- **PEP 8 Compliance**: Style guide enforcement
- **Security Scanning**: eval(), exec(), and injection vulnerabilities
- **Type Hints**: Type annotation recommendations
- **Performance Analysis**: List comprehension and generator optimization
- **Best Practices**: Pythonic code patterns

## 🛠️ Setup and Installation

### Prerequisites
- .NET 8.0 SDK or later
- Visual Studio 2022 or Visual Studio Code
- Azure DevOps account or TFS server access
- OpenAI API key or Azure OpenAI service

### Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-org/CodeReviewAgent.git
   cd CodeReviewAgent
   ```

2. **Configure AI Service**
   Edit `appsettings.json` in the UI project:
   ```json
   {
     "AI": {
       "Provider": "AzureOpenAI",
       "Endpoint": "https://your-instance.openai.azure.com",
       "ApiKey": "your-api-key",
       "ModelName": "gpt-4"
     }
   }
   ```

3. **Build the Solution**
   ```bash
   dotnet build CodeReviewAgent.sln
   ```

4. **Run Tests**
   ```bash
   dotnet test
   ```

5. **Launch the Application**
   ```bash
   cd src/CodeReviewAgent.UI
   dotnet run
   ```

## 🔧 Configuration

### Agent Configuration
Each agent can be individually configured through the settings interface:

```json
{
  "agentId": "csharp-agent",
  "isEnabled": true,
  "reviewConfig": {
    "checkSyntax": true,
    "checkSecurity": true,
    "checkPerformance": true,
    "maxComplexity": 10,
    "maxMethodLength": 50
  }
}
```

### Source Control Configuration
Support for multiple authentication methods:

- **Personal Access Token**: Recommended for Azure DevOps
- **Basic Authentication**: Username/password for TFS
- **OAuth**: For enterprise Azure AD integration
- **Windows Authentication**: For domain-joined TFS scenarios

## 📋 Usage Guide

### Initial Setup
1. **Launch Application**: Start the Code Review Agent
2. **Connect to Source Control**: Use File → Connect to configure Azure DevOps/TFS
3. **Test Connection**: Verify connectivity before proceeding
4. **Configure Agents**: Adjust agent settings in Tools → Agent Configuration

### Running a Review
1. **Select Repository**: Ensure connection to correct project/repository
2. **Start Review**: Click "Start Review" or use Review → Start Review
3. **Enter Pull Request ID**: Specify the PR to review
4. **Monitor Progress**: Watch real-time progress in the main window
5. **Review Results**: Examine findings in the results panel
6. **Post Comments**: Choose whether to post comments to the PR

### Advanced Features
- **Export Results**: Save review results in JSON or CSV format
- **Agent Management**: Enable/disable specific agents per project
- **Custom Rules**: Configure per-agent review rules and thresholds
- **Batch Processing**: Review multiple pull requests sequentially

## 🔌 MCP Protocol Integration

The system uses the Model Context Protocol for standardized communication:

### Supported Operations
- `sourceControl/getRepositories`: List available repositories
- `sourceControl/getPullRequests`: Get pull request information
- `sourceControl/getChangedFiles`: Retrieve modified files
- `sourceControl/postReviewComments`: Post review comments
- `sourceControl/updatePullRequestStatus`: Update PR approval status

### Custom MCP Server
Implement your own MCP server for custom source control systems:

```csharp
public class CustomMcpServer : IMcpService
{
    public async Task<T> SendRequestAsync<T>(string method, object parameters)
    {
        // Custom implementation
    }
}
```

## 🧪 Testing

### Unit Tests
Comprehensive test coverage for all agents and services:

```bash
dotnet test --collect:"XPlat Code Coverage"
```

### Integration Tests
End-to-end testing with mock source control systems:

```bash
dotnet test --filter "Category=Integration"
```

### Performance Tests
Load testing for concurrent review scenarios:

```bash
dotnet test --filter "Category=Performance"
```

## 🚀 Extending the System

### Adding New Language Agents

1. **Create Agent Class**
   ```csharp
   public class JavaCodeReviewAgent : BaseCodeReviewAgent
   {
       public override string AgentId => "java-agent";
       public override List<string> SupportedLanguages => new() { "java" };
       
       protected override async Task<List<ReviewComment>> AnalyzeCodeAsync(
           CodeFile codeFile, AgentConfiguration config, CancellationToken cancellationToken)
       {
           // Implement Java-specific analysis
       }
   }
   ```

2. **Register Agent**
   ```csharp
   services.AddTransient<JavaCodeReviewAgent>();
   // Add to agent collection in DI configuration
   ```

### Custom Review Rules

Create custom rules by implementing the analysis methods:

```csharp
private async Task<List<ReviewComment>> CheckCustomRuleAsync(
    List<string> lines, CancellationToken cancellationToken)
{
    var comments = new List<ReviewComment>();
    // Implement custom logic
    return comments;
}
```

## 📊 Monitoring and Analytics

### Review Metrics
The system tracks comprehensive metrics:
- Files reviewed per session
- Issues found by category and severity
- Agent performance and accuracy
- Review completion times

### Reporting
Generate detailed reports:
- **Summary Reports**: High-level statistics
- **Detailed Analysis**: Per-file breakdown
- **Trend Analysis**: Historical performance
- **Agent Effectiveness**: Comparative analysis

## 🔒 Security Considerations

### Secure Configuration
- Store API keys in secure configuration
- Use managed identities where possible
- Implement proper authentication for source control

### Data Privacy
- No code content stored permanently
- Secure transmission of review data
- Configurable data retention policies

## 🤝 Contributing

### Development Guidelines
1. Follow existing code patterns and conventions
2. Write comprehensive unit tests
3. Update documentation for new features
4. Use semantic versioning for releases

### Pull Request Process
1. Fork the repository
2. Create feature branch
3. Implement changes with tests
4. Submit pull request with description

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

### Documentation
- [User Guide](docs/user-guide.md)
- [Developer Guide](docs/developer-guide.md)
- [API Reference](docs/api-reference.md)

### Community
- [GitHub Issues](https://github.com/your-org/CodeReviewAgent/issues)
- [Discussions](https://github.com/your-org/CodeReviewAgent/discussions)
- [Wiki](https://github.com/your-org/CodeReviewAgent/wiki)

---

**Code Review Agent** - Intelligent, automated code review for modern development teams.