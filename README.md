# Log Archive Tool 
###[Visit testing branch on this repo for sample demo code]

A command-line utility for archiving log files into timestamped compressed archives. This tool helps maintain system cleanliness by compressing old logs while preserving them for future reference.

## Features

- **Simple CLI Interface**: Easy-to-use command-line tool
- **Automatic Compression**: Creates `.tar.gz` archives using system tar command
- **Timestamped Archives**: Archives are named with creation date and time
- **Operation Logging**: Logs all archive operations for audit trail
- **Smart Exclusion**: Automatically excludes existing archive directories to prevent recursion
- **Cross-Platform**: Works on Unix-based systems (Linux, macOS)

## Installation

### Prerequisites

- Python 3.6 or higher
- `tar` command (available on most Unix-based systems)

### Setup

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd log-archive-tool
   ```

2. Make the script executable:
   ```bash
   chmod +x log-archive
   ```

3. Optionally, add to your PATH for system-wide access:
   ```bash
   sudo cp log-archive /usr/local/bin/
   ```

## Usage

### Basic Usage

```bash
./log-archive <log-directory>
```

### Examples

Archive logs from the system log directory:
```bash
./log-archive /var/log
```

Archive logs from a custom application directory:
```bash
./log-archive /path/to/app/logs
```

Archive the demo logs included in this repository:
```bash
./log-archive demo_logs
```

### Output

The tool creates:
- An `archives/` directory in your current working directory
- A timestamped archive file (e.g., `logs_archive_20240816_100648.tar.gz`)
- An operation log at `archives/archive.log`

## Archive Format

Archives are named using the following format:
```
logs_archive_YYYYMMDD_HHMMSS.tar.gz
```

Where:
- `YYYY`: 4-digit year
- `MM`: 2-digit month
- `DD`: 2-digit day
- `HH`: 2-digit hour (24-hour format)
- `MM`: 2-digit minute
- `SS`: 2-digit second

## Development

This project includes a development container configuration for easy setup:

### Using Dev Container

1. Open the project in VS Code
2. Install the "Dev Containers" extension
3. Press `Ctrl+Shift+P` and select "Dev Containers: Reopen in Container"

The dev container provides:
- Java 21 runtime environment
- Maven 3.8.6
- Gradle build tool

### Testing

Test the tool with the included demo logs:

```bash
# Run the tool on demo data
./log-archive demo_logs

# Check the created archive
ls -la archives/

# View the operation log
cat archives/archive.log
```

## Error Handling

The tool handles various error conditions:

- **Missing directory**: Returns error code 2 if the specified directory doesn't exist
- **Invalid path**: Returns error code 2 if the path is not a directory
- **Missing tar command**: Returns error code 1 if tar is not available
- **Archive creation failure**: Returns error code 1 if tar fails to create the archive

All errors are logged to `archives/archive.log` with timestamps.

## Advanced Features

Future enhancements could include:

- **Email notifications**: Send archive completion notifications
- **Remote storage**: Upload archives to cloud storage or remote servers
- **Automated scheduling**: Integration with cron for automatic archiving
- **Retention policies**: Automatic cleanup of old archives
- **Configuration files**: Support for custom archive settings

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

Copyright (c) 2025 ReddyNextDoor

---

**Note**: This tool is designed for Unix-based systems and requires the `tar` command to be available in the system PATH.
