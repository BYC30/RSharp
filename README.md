# RSharp

A remote C# interpreter based on reflection, allowing network-based command execution and real-time result retrieval.

## Description

RSharp is a lightweight C# interpreter that enables remote code execution through network protocols. Built on the .NET reflection API, it provides a REPL (Read-Eval-Print-Loop) environment accessible over the network, allowing developers to execute C# code snippets, inspect objects, and interact with .NET assemblies remotely.

## Features

- **Remote Execution**: Execute C# code remotely through network connections
- **Reflection-based**: Leverages .NET reflection for dynamic code interpretation
- **Real-time Results**: Immediate feedback and result streaming
- **Secure Communication**: Built-in authentication and encrypted connections
- **Session Management**: Persistent sessions with context preservation
- **Assembly Loading**: Dynamic loading of external assemblies and references
- **Error Handling**: Comprehensive error reporting and exception handling

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/RSharp.git

# Navigate to the project directory
cd RSharp

# Build the project
dotnet build

# Run the server
dotnet run --project RSharp.Server
```

## Usage

### Starting the Server

```bash
RSharp.Server --port 9000 --host 0.0.0.0
```

### Connecting with Client

```csharp
// Connect to RSharp server
var client = new RSharpClient("localhost", 9000);
await client.ConnectAsync();

// Execute C# code
var result = await client.ExecuteAsync("Math.Pow(2, 10)");
Console.WriteLine(result); // Output: 1024

// Execute multi-line code
var code = @"
var list = new List<int> { 1, 2, 3, 4, 5 };
list.Where(x => x % 2 == 0).Sum()
";
var sum = await client.ExecuteAsync(code);
Console.WriteLine(sum); // Output: 6
```

### Command Line Interface

```bash
# Connect to RSharp server via CLI
RSharp.CLI connect localhost:9000

# Execute commands
> var x = 10;
> var y = 20;
> x + y
30

> DateTime.Now
2025-06-09 10:30:45

> exit
```

## Configuration

Create a `rsharp.config.json` file:

```json
{
  "server": {
    "port": 9000,
    "host": "0.0.0.0",
    "maxConnections": 100,
    "timeout": 30000
  },
  "security": {
    "enableAuthentication": true,
    "enableSSL": true,
    "certificatePath": "./certs/server.pfx"
  },
  "execution": {
    "maxExecutionTime": 60000,
    "memoryLimit": "100MB",
    "allowUnsafeCode": false
  }
}
```

## Security Considerations

- Always use authentication in production environments
- Enable SSL/TLS for encrypted communication
- Implement proper access controls and code execution restrictions
- Regularly update dependencies and security patches
- Monitor and log all remote execution activities

## Requirements

- .NET 8.0 or higher
- Windows, Linux, or macOS

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Disclaimer

RSharp allows remote code execution which can be a security risk if not properly configured. Always ensure proper security measures are in place before deploying to production environments.
