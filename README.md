# Git Account Manager

A ZSH script to manage multiple GitHub accounts on a single machine.

## Features

- Manage multiple GitHub accounts easily
- Switch between different Git profiles
- Automatic SSH key generation and configuration
- View current Git configuration

## Installation

1. Clone the repository:
```bash
git clone git@github.com:yourusername/git-account-manager.git
```

2. Make the script executable:
```bash
chmod +x git-account
```

3. Move to a directory in your PATH:
```bash
sudo mv git-account /usr/local/bin/
```

## Usage

### Add a new account
```bash
git-account add
```

### Switch between accounts
```bash
git-account switch 
```

### View current configuration
```bash
git-account current
```
