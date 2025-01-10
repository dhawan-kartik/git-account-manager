# Git Account Manager

## Overview
Git Account Manager is a command-line tool designed to simplify the management of multiple GitHub accounts on a single system. It provides functionality to add, switch between, and view the current GitHub account configuration, making it easier to maintain separate personal and professional GitHub identities.

## Features
- Add new GitHub accounts with associated SSH keys
- Switch between different GitHub accounts
- View current Git configuration
- Automatic SSH key generation and configuration
- Persistent configuration storage

## Installation

### Prerequisites
- Zsh shell
- Git
- SSH client
- Basic understanding of Git and SSH concepts

### Setup Steps

Method 1: Direct Installation
```bash
# Clone the repository
git clone https://github.com/dhawan-kartik/git-account-manager.git

# Move into the directory
cd git-account-manager

# Make the script executable
chmod +x git-account

# Move to system bin (requires sudo)
sudo mv git-account /usr/local/bin/
```

Method 2: Manual Download
1. Download the script from [GitHub Repository](https://github.com/dhawan-kartik/git-account-manager)
2. Make it executable: `chmod +x git-account`
3. Move to system bin: `sudo mv git-account /usr/local/bin/`

Verify installation:
```bash
git-account
```

## Usage

### Adding a New Account

```bash
git-account add
```

This command will:
1. Prompt for account details (name, email, GitHub username)
2. Generate a new SSH key pair
3. Configure SSH for the account
4. Store account information in `~/.git-accounts`

After adding an account:
1. Copy the displayed public key
2. Add it to your GitHub account:
   - Go to GitHub Settings → SSH and GPG keys
   - Click "New SSH key"
   - Paste the copied key

### Switching Accounts

```bash
git-account switch <account_name>
```

Example:
```bash
git-account switch main
```

This will:
- Update global Git configuration
- Configure SSH to use the correct key
- Display the new active configuration

### Viewing Current Configuration

```bash
git-account current
```

Displays:
- Current Git username
- Current Git email

## Configuration Files

### Git Accounts Configuration
- Location: `~/.git-accounts`
- Format: `account_name:email:ssh_key_name:github_username`
- Example:
  ```
  main:john@example.com:id_rsa_main:johnsmith
  work:john@company.com:id_rsa_work:john-company
  ```

### SSH Configuration
- Location: `~/.ssh/config`
- Added automatically for each account
- Format:
  ```
  Host github.com-<account_name>
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_rsa_<account_name>
  ```

## Repository Usage

When cloning repositories, use account-specific host configurations:

```bash
# For main account
git clone git@github.com-main:username/repo.git

# For work account
git clone git@github.com-work:username/repo.git
```

## Troubleshooting

### SSH Key Issues
1. Verify SSH key exists:
   ```bash
   ls ~/.ssh/id_rsa_<account_name>*
   ```

2. Test SSH connection:
   ```bash
   ssh -T git@github.com-<account_name>
   ```

### Configuration Issues
1. Check Git configuration:
   ```bash
   git config --global --list
   ```

2. Verify account in config file:
   ```bash
   cat ~/.git-accounts
   ```

### Common Problems and Solutions

1. **Permission Denied (publickey)**
   - Ensure SSH key is added to GitHub
   - Check SSH key permissions (should be 600)
   - Verify SSH configuration

2. **Wrong Account Used for Push**
   - Check current Git configuration
   - Verify repository remote URL uses correct host
   - Switch to correct account using `git-account switch`

3. **SSH Key Generation Fails**
   - Ensure ~/.ssh directory exists
   - Check write permissions
   - Verify sufficient disk space

## Best Practices

1. Use meaningful account names
2. Keep separate SSH keys for each account
3. Regularly backup ~/.git-accounts and SSH keys
4. Use repository-specific configurations when needed
5. Verify active account before making commits

## Security Considerations

1. Protect SSH private keys
   ```bash
   chmod 600 ~/.ssh/id_rsa_*
   ```

2. Use strong passphrases for SSH keys
3. Regular backup of configuration
4. Avoid sharing SSH private keys
5. Keep Git Account Manager script up to date

## Uninstallation

To remove Git Account Manager:

1. Remove the script:
   ```bash
   sudo rm /usr/local/bin/git-account
   ```

2. Remove configurations (optional):
   ```bash
   rm ~/.git-accounts
   ```

3. Remove SSH keys (optional):
   ```bash
   rm ~/.ssh/id_rsa_*
   ```

## Contributing

Found a bug or want to contribute? Please visit our [GitHub repository](https://github.com/dhawan-kartik/git-account-manager) and submit issues or pull requests.

## License

This script is released under the MIT License. See LICENSE file for details.