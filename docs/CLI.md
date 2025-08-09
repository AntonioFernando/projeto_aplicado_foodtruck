# 🚚 Food Truck CLI Documentation

[![Python Version](https://img.shields.io/badge/python-3.13+-blue.svg)](https://python.org)
[![CLI Framework](https://img.shields.io/badge/CLI-Cyclopts-green.svg)](https://github.com/BrianPugh/cyclopts)
[![Architecture](https://img.shields.io/badge/architecture-Clean%20Architecture-orange.svg)](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

> **Modern CLI for Food Truck Management System** - Built with Clean Architecture, SOLID principles, and comprehensive testing.

## 📋 Table of Contents

- [🎯 Overview](#-overview)
- [🚀 Quick Start](#-quick-start)
- [📦 Installation](#-installation)
- [🛠️ Commands Reference](#️-commands-reference)
- [🏗️ Architecture](#️-architecture)
- [💡 Examples](#-examples)
- [🧪 Testing](#-testing)
- [📚 Troubleshooting](#-troubleshooting)

## 🎯 Overview

The Food Truck CLI is a comprehensive command-line interface for managing the Food Truck Management System. It provides tools for:

- **System Health Monitoring** - Check database connections and system status
- **User Management** - Create and manage admin users
- **Database Operations** - Handle migrations, schema changes, and database setup
- **Shell Configuration** - Easy setup for direct CLI access
- **Completion Support** - Tab completion for bash, zsh, and fish shells

### ✨ Key Features

- 🏗️ **Clean Architecture** - Follows SOLID principles with clear separation of concerns
- 🧪 **100% Tested** - Comprehensive test coverage for all components
- 🎨 **Rich Output** - Beautiful, colored console output with emojis and formatting
- 🐚 **Shell Integration** - Native completion support for major shells
- 🔒 **Secure** - Safe database operations with validation and error handling
- ⚡ **Fast** - Optimized for quick operations and minimal startup time
- 🎯 **Auto-Setup** - Automatically configures convenient aliases on first use

## 🚀 Quick Start

### Prerequisites

- Python 3.13+
- PostgreSQL (for database operations)
- Virtual environment activated

### Basic Usage

```bash
# First time: Auto-sets up convenient aliases
uv run python -m projeto_aplicado.cli.app

# After setup, use short aliases
source ~/.zshrc  # or ~/.bashrc
ftcli health
ft-admin list-admins
ft-db status

# Or continue using full commands
uv run python -m projeto_aplicado.cli.app health
uv run python -m projeto_aplicado.cli.app database init
uv run python -m projeto_aplicado.cli.app admin create admin admin@foodtruck.com admin123 "System Administrator"
```

## 📦 Installation

### 🚀 Quick Setup (Recommended)

```bash
# 1. From project root
cd /path/to/foodtruck
source .venv/bin/activate

# 2. First run auto-configures aliases
uv run python -m projeto_aplicado.cli.app

# 3. Reload shell to use short commands
source ~/.zshrc  # or ~/.bashrc

# 4. Now use convenient aliases
ftcli health
ft-admin list-admins
```

### 🔧 Alternative: Global CLI Access

```bash
# Install globally with uv tool
uv tool install --editable .

# Now available globally
foodtruck-cli --help

# Auto-configure your shell (if needed)
foodtruck-cli setup install
```

## 🎯 Auto-Setup Feature

The CLI automatically configures convenient aliases on first use to improve your productivity:

### What Happens on First Use

1. **Detection** - Checks if aliases are already configured
2. **Shell Detection** - Identifies your shell (bash, zsh, fish)
3. **Auto-Configuration** - Adds aliases to your shell config
4. **Success Feedback** - Shows what was configured

### Auto-Generated Aliases

| Alias | Full Command | Description |
|-------|-------------|-------------|
| `ftcli` | `cd /project && uv run python -m projeto_aplicado.cli.app` | Main CLI |
| `ft-health` | `ftcli health` | Quick health check |
| `ft-admin` | `ftcli admin` | Admin commands |
| `ft-db` | `ftcli database` | Database operations |
| `ft-setup` | `ftcli setup` | Setup commands |
| `ft-completions` | `ftcli completions` | Completion management |

### Benefits

- ✅ **Works from anywhere** - Aliases include `cd` to project directory
- ✅ **No manual setup** - Configured automatically on first use
- ✅ **Shell-aware** - Detects and configures the right shell
- ✅ **One-time only** - Won't duplicate configuration on subsequent uses
- ✅ **Pure uv workflow** - Uses `uv run` for maximum compatibility

### Manual Control

```bash
# Skip auto-setup by using setup commands directly
uv run python -m projeto_aplicado.cli.app setup install --help
uv run python -m projeto_aplicado.cli.app setup alias

# Remove aliases (manual)
# Edit ~/.zshrc or ~/.bashrc and remove "Food Truck CLI aliases" section
```

## 🛠️ Commands Reference

### 🏥 Health Command

Check system health and connectivity.

```bash
# Basic health check (with aliases)
ft-health

# Using full command
uv run python -m projeto_aplicado.cli.app health

# Check with custom database host
ftcli health --db-host mydb.example.com
```

**What it checks:**
- ✅ Database connectivity
- ✅ Admin user presence
- ✅ Application settings
- ✅ System configuration

**Output Example:**
```
🏥 System Health Check
✓ Database connection: OK
✓ Admin users: 2 found
✓ Settings loaded: OK
  Database: foodtruck
  Host: localhost:5432
🎉 All 3 health checks passed!
```

### 👥 Admin Commands

Manage administrative users in the system.

#### Create Admin User

```bash
foodtruck-cli admin create <username> <email> <password> <full_name> [--force]
```

**Examples:**
```bash
# Create basic admin (with aliases)
ft-admin create admin admin@foodtruck.com admin123 "System Administrator"

# Force create (overwrite existing)
ft-admin create superadmin admin@company.com secret123 "Super Admin" --force

# Using full command
uv run python -m projeto_aplicado.cli.app admin create admin admin@foodtruck.com admin123 "System Administrator"
```

#### Check Admin User

```bash
foodtruck-cli admin check <email>
```

**Example:**
```bash
foodtruck-cli admin check admin@foodtruck.com
# Output: ✓ User found: admin (admin@foodtruck.com) - System Administrator
```

#### List Admin Users

```bash
foodtruck-cli admin list-admins
```

**Output Example:**
```
✓ Found 2 admin user(s):
  • admin (admin@foodtruck.com) - System Administrator
  • superadmin (admin@company.com) - Super Administrator
```

### 💾 Database Commands

Handle database migrations and schema management.

#### Initialize Database

```bash
foodtruck-cli database init
```

Sets up database schema and runs all migrations.

#### Database Status

```bash
foodtruck-cli database status
```

**Output Example:**
```
📊 Database Status
✓ Database connection: OK
✓ Alembic configuration: OK
✓ Migrations directory: Found
ℹ Current migration: ca713c51cd3c (head)
```

#### Migration Management

```bash
# Upgrade to latest
foodtruck-cli database upgrade

# Upgrade to specific revision
foodtruck-cli database upgrade abc123

# Downgrade one revision
foodtruck-cli database downgrade -1

# Show current revision
foodtruck-cli database current

# Show migration history
foodtruck-cli database history
```

#### Create Migration

```bash
foodtruck-cli database create "add user profile table"
```

#### Reset Database (⚠️ Destructive)

```bash
foodtruck-cli database reset --confirm
```

### ⚙️ Setup Commands

Configure shell environment for optimal CLI usage.

#### Show PATH Configuration

```bash
foodtruck-cli setup path
```

Shows current PATH setup and provides manual installation instructions.

#### Generate Shell Aliases

```bash
# Auto-detect shell
foodtruck-cli setup alias

# Specific shell
foodtruck-cli setup alias zsh
```

**Generated aliases:**
- `ftcli` → `foodtruck-cli`
- `ft-health` → `foodtruck-cli health`
- `ft-admin` → `foodtruck-cli admin`
- `ft-db` → `foodtruck-cli database`

#### Auto-Install Shell Configuration

```bash
# Auto-configure current shell
foodtruck-cli setup install

# Force overwrite existing config
foodtruck-cli setup install --force

# Specific shell
foodtruck-cli setup install zsh
```

#### Check Shell Configuration

```bash
foodtruck-cli setup check
```

Shows current shell setup status and accessibility.

### 🔧 Completions Commands

Manage shell tab completions.

#### Install Completions

```bash
# Auto-install for current shell
foodtruck-cli completions install

# Specific shell
foodtruck-cli completions install bash
foodtruck-cli completions install zsh
foodtruck-cli completions install fish
```

#### Generate Completion Scripts

```bash
# Output to stdout
foodtruck-cli completions generate bash

# Save to file
foodtruck-cli completions generate zsh --output foodtruck-cli.zsh
```

#### Check Completion Status

```bash
foodtruck-cli completions status
```

**Output Example:**
```
📊 Completions Status
Shell Information:
ℹ Current shell: zsh
ℹ Completion support: True

Installation Status:
✅ zsh: Installed at /home/user/.zsh/completion/_foodtruck-cli
⚠️ bash: Not installed
⚠️ fish: Not installed

Testing:
💡 Test completions: foodtruck-cli <TAB><TAB>
```

#### Uninstall Completions

```bash
# Remove from current shell
foodtruck-cli completions uninstall

# Remove from all shells
foodtruck-cli completions uninstall all
```

### ℹ️ Version Command

```bash
foodtruck-cli version
```

**Output:**
```
🚚 Food Truck Management System
Version: 1.0.0
Python CLI Framework: Cyclopts
Database: PostgreSQL with SQLModel
Web Framework: FastAPI
```

## 🏗️ Architecture

The CLI is built using **Clean Architecture** principles with clear separation of concerns:

### 📁 Directory Structure

```
projeto_aplicado/cli/
├── 📱 app.py                   # Main CLI application factory
├── 🏛️ base/                    # Abstract base classes (SOLID)
│   ├── command.py             # BaseCommand (SRP + OCP)
│   └── service.py             # BaseService (SRP + ISP)
├── 🎮 commands/                # CLI commands (SRP)
│   ├── admin.py               # Admin user management
│   ├── completions.py         # Shell completion management
│   ├── database.py            # Database and migration commands
│   ├── health.py              # System health checks
│   └── setup.py               # Shell setup and configuration
├── ⚙️ services/                # Business logic services (SRP + DIP)
│   ├── completions.py         # Completion script generation
│   ├── database.py            # Database operations
│   ├── health.py              # Health check logic
│   ├── migration.py           # Migration management
│   ├── shell.py               # Shell configuration
│   └── user.py                # User operations
└── 🧪 tests/                   # Comprehensive test suite
    ├── test_app.py            # Integration tests
    ├── test_commands.py       # Command unit tests
    ├── test_services.py       # Service unit tests
    └── test_integration.py    # End-to-end tests
```

### 🎯 SOLID Principles Implementation

- **🔧 Single Responsibility**: Each command and service has one clear purpose
- **📖 Open/Closed**: Easy to extend with new commands without modifying existing code
- **🔄 Liskov Substitution**: All commands and services follow consistent interfaces
- **⚙️ Interface Segregation**: Focused, minimal interfaces for commands and services
- **🔀 Dependency Inversion**: Commands depend on service abstractions, not implementations

### 🧪 Testing Strategy

- **Unit Tests**: 100% coverage for all services and commands
- **Integration Tests**: End-to-end command execution
- **Mocking**: Proper isolation of external dependencies
- **Error Scenarios**: Comprehensive error handling coverage

## 💡 Examples

### Complete Setup Workflow

```bash
# 1. First run (auto-configures aliases)
uv run python -m projeto_aplicado.cli.app

# 2. Reload shell
source ~/.zshrc  # or ~/.bashrc

# 3. Check system health (using aliases)
ft-health

# 4. Initialize database
ft-db init

# 5. Create admin user
ft-admin create admin admin@foodtruck.com admin123 "System Administrator"

# 6. Verify admin creation
ft-admin check admin@foodtruck.com

# 7. Install shell completions (optional)
ft-completions install
```

### Database Migration Workflow

```bash
# Check current status
foodtruck-cli database status

# Create new migration
foodtruck-cli database create "add user profile fields"

# Review migration history
foodtruck-cli database history

# Apply migrations
foodtruck-cli database upgrade

# Verify current state
foodtruck-cli database current
```

### Development Environment Setup

```bash
# Install project dependencies
uv pip install -e .[dev]

# Set up shell access
foodtruck-cli setup install

# Install completions
foodtruck-cli completions install

# Verify everything works
foodtruck-cli health
```

### Production Deployment

```bash
# Check health with production database
foodtruck-cli health --db-host prod-db.company.com

# Initialize production database
foodtruck-cli database init --db-host prod-db.company.com

# Create production admin
foodtruck-cli admin create prod_admin admin@company.com secure_password "Production Administrator"

# Verify setup
foodtruck-cli admin list-admins
```

## 🧪 Testing

### Running Tests

```bash
# All CLI tests
uv run pytest projeto_aplicado/cli/tests/ -v

# Specific test categories
uv run pytest projeto_aplicado/cli/tests/test_commands.py -v
uv run pytest projeto_aplicado/cli/tests/test_services.py -v
uv run pytest projeto_aplicado/cli/tests/test_integration.py -v

# With coverage
uv run pytest projeto_aplicado/cli/tests/ --cov=projeto_aplicado.cli --cov-report=html
```

### Test Structure

- **71 dedicated CLI tests** with 100% coverage
- **Unit tests** for individual components
- **Integration tests** for complete workflows
- **Mock strategies** for external dependencies

## 📚 Troubleshooting

### Common Issues

#### Command Not Found

```bash
# Issue: foodtruck-cli: command not found
# Solution: Activate virtual environment
source .venv/bin/activate

# Or setup permanent access
foodtruck-cli setup install
```

#### Database Connection Issues

```bash
# Issue: Database connection failed
# Check: Is PostgreSQL running?
sudo systemctl status postgresql

# Check: Are credentials correct?
foodtruck-cli health --db-host localhost

# Check: Environment variables
echo $POSTGRES_HOSTNAME
echo $POSTGRES_DB
```

#### Migration Issues

```bash
# Issue: Migration conflicts
# Solution: Check current state
foodtruck-cli database status
foodtruck-cli database history

# Reset if necessary (⚠️ destructive)
foodtruck-cli database reset --confirm
foodtruck-cli database init
```

#### Permission Issues

```bash
# Issue: Permission denied when installing completions
# Solution: Check directory permissions
ls -la ~/.zsh/completion/
chmod 755 ~/.zsh/completion/

# Or try user-specific installation
foodtruck-cli completions install --shell zsh
```

### Debug Mode

For detailed error information, use Python's verbose mode:

```bash
uv run python -v -m projeto_aplicado.cli.app <command>
```

### Getting Help

- **Command help**: `foodtruck-cli <command> --help`
- **General help**: `foodtruck-cli --help`
- **Version info**: `foodtruck-cli version`
- **Health check**: `foodtruck-cli health`

### Environment Variables

The CLI respects these environment variables:

```bash
# Database configuration
POSTGRES_HOSTNAME=localhost     # Database host
POSTGRES_DB=foodtruck          # Database name
POSTGRES_USER=postgres         # Database user
POSTGRES_PASSWORD=password     # Database password

# Application settings
SECRET_KEY=your-secret-key     # JWT secret key
```

---

## 🤝 Contributing

The CLI follows strict architectural principles. When contributing:

1. **Follow Clean Architecture** - Keep commands thin, put logic in services
2. **Write Tests** - All new features must have 100% test coverage
3. **Use Type Hints** - Full type annotation is required
4. **Follow SOLID** - Each class should have a single responsibility
5. **Rich Output** - Use the Rich console for beautiful, informative output

### Adding New Commands

1. Create command class in `commands/`
2. Create corresponding service in `services/`
3. Register in `app.py`
4. Add comprehensive tests
5. Update this documentation

---

<div align="center">

**Built with ❤️ using Clean Architecture and SOLID principles**

[🐛 Report Bug](https://github.com/bentoluizv/projeto_aplicado_foodtruck/issues) • 
[💡 Request Feature](https://github.com/bentoluizv/projeto_aplicado_foodtruck/issues) • 
[📖 Main Documentation](../README.md)

</div>
