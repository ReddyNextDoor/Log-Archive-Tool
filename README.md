# Log Archive Tool - Testing Branch

This branch contains comprehensive testing scenarios and validation for the log archive tool. The tool is **format-agnostic** and can archive any file type or directory structure.

## What This Tool Accepts

The log archive tool doesn't parse file contents - it simply compresses whatever you point it at using `tar`. This means it accepts:

### ✅ Supported File Formats
- **Traditional logs**: `.log`, `.txt` files
- **Structured logs**: `.json`, `.xml` files  
- **Data logs**: `.csv`, `.tsv` files
- **Binary files**: Any binary data
- **Mixed formats**: All file types in same directory
- **Special characters**: Files with spaces, symbols (@#$), etc.

### ✅ Directory Structures
- Nested subdirectories (any depth)
- Mixed file types in same directory
- Empty files and directories
- Complex hierarchies

## Test Files Included

This branch includes comprehensive test data:

```
test_logs/
├── application.log          # Standard application logs
├── access.log              # Apache/Nginx style access logs
├── system.json             # JSON structured logs
├── metrics.csv             # CSV data logs
├── large.log               # Large binary file (1MB)
├── file with spaces.log    # Filename with spaces
├── file-with-symbols@#$.log # Special characters
└── database/
    └── query.log           # Nested directory structure
```

## Testing Commands

### Basic Testing
```bash
# Test with comprehensive test data
./log-archive test_logs

# Test with demo data
./log-archive demo_logs

# Test with single file
mkdir single_file_test
echo "2025-09-20 Test log entry" > single_file_test/test.log
./log-archive single_file_test
```

### Error Testing
```bash
# Test non-existent path (should return error code 2)
./log-archive /nonexistent/path

# Test file instead of directory (should return error code 2)
touch test_file.log
./log-archive test_file.log
```

### Archive Inspection
```bash
# List all created archives
ls -la archives/

# View archive contents (replace TIMESTAMP with actual timestamp)
tar -tzf archives/logs_archive_TIMESTAMP.tar.gz

# Extract archive for inspection
mkdir temp_extract
tar -xzf archives/logs_archive_TIMESTAMP.tar.gz -C temp_extract
ls -la temp_extract/

# View operation log
cat archives/archive.log
```

## Test Results Validation

### Expected Behavior
1. **Archive Creation**: Creates timestamped `.tar.gz` files in `archives/` directory
2. **Content Preservation**: All files and directory structures preserved exactly
3. **Logging**: Each operation logged with timestamp to `archives/archive.log`
4. **Error Handling**: Proper error codes and messages for invalid inputs

### Sample Test Output
```bash
➜ ./log-archive test_logs
/Users/[user]/Log-Archive-Tool/archives/logs_archive_20250920_144907.tar.gz

➜ tar -tzf archives/logs_archive_20250920_144907.tar.gz
./
./large.log
./database/
./file with spaces.log
./metrics.csv
./file-with-symbols@#$.log
./access.log
./application.log
./system.json
./database/query.log
```

## Performance Testing

### Large File Handling
```bash
# Create larger test files
dd if=/dev/zero of=test_logs/large.log bs=1M count=10

# Test with many small files
for i in {1..100}; do
    echo "Log entry $i at $(date)" > test_logs/small_$i.log
done

./log-archive test_logs
```

### Directory Depth Testing
```bash
# Create deep nested structure
mkdir -p test_logs/level1/level2/level3/level4
echo "Deep nested log" > test_logs/level1/level2/level3/level4/deep.log
./log-archive test_logs
```

## Archive Format Verification

Archives follow the naming convention:
```
logs_archive_YYYYMMDD_HHMMSS.tar.gz
```

Example: `logs_archive_20250920_144907.tar.gz`
- `20250920`: September 20, 2025
- `144907`: 14:49:07 (2:49:07 PM)

## Cleanup Commands

```bash
# Remove test artifacts
rm -rf archives/ temp_extract/ single_file_test/
rm test_logs/large.log

# Reset to clean state
git checkout -- test_logs/
```

## Branch Purpose

This testing branch demonstrates:
- **Format flexibility**: Tool works with any file format
- **Robustness**: Handles edge cases like special characters, large files
- **Reliability**: Consistent archive creation and logging
- **Error handling**: Proper validation and error reporting

The comprehensive test suite validates that the log archive tool is production-ready for any log archiving scenario.