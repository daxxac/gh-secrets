# GitHub Secrets Import Script

This script automates the process of importing environment variables from a `.env` file into GitHub repository secrets.

## Prerequisites

- GitHub CLI (`gh`) installed on your machine
- Git repository initialized and connected to GitHub
- `.env` file in your project root
- Authentication with GitHub

## Installation

1. If you don't have GitHub CLI installed:

```bash
# macOS
brew install gh

# Linux (Ubuntu/Debian)
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

2. Clone the script:

```bash
curl -o gh-secrets-script.sh https://raw.githubusercontent.com/daxxac/gh-secrets/main/.gh-secrets-script
chmod +x gh-secrets-script.sh
```

## Usage

1. Make sure you have a `.env` file in your project directory with secrets in the following format:
```env
SECRET_NAME=secret_value
ANOTHER_SECRET=another_value
```

2. Run the script:
```bash
./gh-secrets-script.sh
```

The script will:
- Check if GitHub CLI is installed
- Verify authentication with GitHub
- Read each line from `.env`
- Create corresponding secrets in your GitHub repository
- Skip empty lines and comments
- Handle values with spaces and quotes

## Features

- Automatically installs GitHub CLI if not present
- Handles authentication with GitHub
- Processes multi-line values
- Skips empty lines and comments
- Strips whitespace and quotes from values
- Provides feedback for each created secret

## Example

```bash
# Your .env file
API_KEY="your-api-key"
DATABASE_URL=postgresql://user:pass@localhost:5432/db
# This is a comment
EMPTY_VAR=

# Run the script
./gh-secrets-script.sh

# Output
Creating secret: API_KEY
Creating secret: DATABASE_URL
✅ Secrets imported successfully!
```

## Security Notes

- The script does not store or log any secret values
- Secrets are transmitted securely using GitHub's API
- Make sure your `.env` file is listed in `.gitignore`
- Delete or secure your `.env` file after importing secrets

## Troubleshooting

If you encounter authentication issues:
```bash
gh auth login
```

If you need to verify current authentication:
```bash
gh auth status
```

## Contributing

Feel free to submit issues and enhancement requests!

## License

This script is released under the MIT License. See the LICENSE file for details.
