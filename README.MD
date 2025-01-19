# Obsidian Server Portal Configuration Library

This is a Rust library designed for the [Obsidian Server Portal](https://github.com/Obsidian-Minecraft-Server-Portal), a server panel for managing Minecraft environments. The library provides a configuration management system for the portal and its related services.

This library can only be added as a Git dependency.

## Features

- **Configuration Management**:
    - Handles loading, saving, and generating default configurations.
    - Automatically creates and normalizes directories for servers, backups, and Java installations.

- **Static Configuration Instance**:
    - Uses [`lazy_static`](https://docs.rs/lazy_static/) to provide a static, runtime-loaded configuration.

- **Error Logging**:
    - Includes error handling with logging using the [`log`](https://docs.rs/log/) crate.

## Installation

To include the `configuration` library in your Rust project, add the following to your `Cargo.toml`:

```toml
[dependencies]
configuration = { git = "https://github.com/Obsidian-Minecraft-Server-Portal/configuration.git" }
```

This library uses the `2021` edition of Rust and requires the latest version of its dependencies for compatibility.

## Usage

### Loading Configuration

When integrated into your application, the configuration is automatically loaded at runtime via the `ObsidianConfig` struct:

```rust
use configuration::config::CONFIG;

fn main() {
    println!("Server Port: {}", CONFIG.port);
}
```

### Defining Your Configuration

The `ObsidianConfig` struct includes the following fields:

- **`port`**: `u16`  
  The application's port number (default is `45560`).

- **`port_forward_webui`**: `bool`  
  Whether to enable port forwarding for the web UI (default is `false`).

- **`automatically_port_forward_servers`**: `bool`  
  Whether to enable automatic port forwarding for servers (default is `false`).

- **`servers_directory`**: `String`  
  Directory where Minecraft servers are stored (default is `servers`).

- **`backups_directory`**: `String`  
  Directory where backups are stored (default is `backups`).

- **`java_install_directory`**: `String`  
  Directory where Java is installed (default is `meta/java`).

### Configuration Lifecycle

1. **Default Configuration**:  
   When the application starts, it generates default configuration values if the `app_settings.json` file does not exist or if it encounters parsing errors.

2. **File Storage**:  
   The configuration is stored in `app_settings.json`. Any changes to configuration values are saved back to this file.

### Example: Customizing Configurations

You can create or update the `app_settings.json` file to override default configuration values. Here's an example of a manually customized `app_settings.json`:

```json
{
  "port": 8080,
  "port_forward_webui": true,
  "automatically_port_forward_servers": false,
  "servers_directory": "custom_servers",
  "backups_directory": "custom_backups",
  "java_install_directory": "custom_java_directory"
}
```

### Key Functions

- **`ObsidianConfig::new()`**  
  Loads or creates a new configuration instance.

- **`ObsidianConfig::save()`**  
  Saves the current configuration to `app_settings.json`.

- **`ObsidianConfig::load()`**  
  Loads configuration values from `app_settings.json`. If the file is missing or contains invalid data, defaults are used.

- **`ObsidianConfig::get_default_config()`**  
  Generates the default configuration values and ensures all necessary directories exist.

## Contributing

Contributions are welcome! If you'd like to submit a pull request, open an issue, or report a bug, please visit the [GitHub repository](https://github.com/Obsidian-Minecraft-Server-Portal/configuration).

### Development Setup

To build and run the project locally:

1. Clone the repository:
   ```bash
   git clone https://github.com/Obsidian-Minecraft-Server-Portal/configuration.git
   cd configuration
   ```

2. Build the project:
   ```bash
   cargo build
   ```

3. Run tests:
   ```bash
   cargo test
   ```

## Dependencies

This library uses the following Rust crates:

- [`serde`](https://crates.io/crates/serde) (1.0.210): Serialization and deserialization with derive support.
- [`serde_json`](https://crates.io/crates/serde_json) (1.0.128): JSON parsing and serialization.
- [`lazy_static`](https://crates.io/crates/lazy_static) (1.5.0): Lazy initialization of global static variables.
- [`log`](https://crates.io/crates/log) (0.4.22): Logging support for error and debug messages.
- [`obsidian-common`](https://github.com/Obsidian-Minecraft-Server-Portal/common-lib): Common utilities and traits for the Obsidian ecosystem.

## License

This project is licensed under the LGPL-3.0. See the `LICENSE` file for details.

---

Made with ❤️ by the [Obsidian Server Portal](https://github.com/Obsidian-Minecraft-Server-Portal) team.