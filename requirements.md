# Project Requirements: Log Archive Tool

## Project Description

Build a command-line tool to archive logs on a set schedule by compressing them and storing them in a new directory. This is especially useful for removing old logs and keeping the system clean while maintaining the logs in a compressed format for future reference. This project will help you practice your programming skills, including working with files and directories, and building a simple CLI tool.

The most common location for logs on a Unix-based system is `/var/log`.

---

## Requirements

- **CLI Interface**
  - The tool should run from the command line.
  - Accept the log directory as an argument when running the tool.
  - Example usage:
    ```bash
    log-archive <log-directory>
    ```
    Where `<log-directory>` is the directory containing the logs to be archived.

- **Compression & Storage**
  - The tool should compress the logs in a `.tar.gz` file.
  - The archive file should be stored in a new directory (e.g., `archives/`).

- **Archive Naming**
  - The archive filename should reflect the date and time of creation, e.g.:
    ```
    logs_archive_20240816_100648.tar.gz
    ```

- **Logging Archive Events**
  - The tool should log each archive operation, including the date and time, to a file for reference.

- **Reference**
  - You can learn more about the `tar` command [here](https://www.gnu.org/software/tar/manual/tar.html).

---

## Advanced Features (Optional)

For a more advanced version, consider adding functionality such as:

- Emailing the user updates on archive events.
- Sending the archive to a remote server or cloud storage.
- Scheduling the tool to run automatically (e.g., via `cron`).

---

## Summary

- Provide the log directory as an argument.
- Compress logs into a timestamped `.tar.gz` archive.
- Store the archive in a new directory.
- Log the date and time of each archive operation.
