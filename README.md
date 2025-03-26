# add_api_key

**add_api_key** is a universal Bash script that loads API keys (or any export commands) into your current shell environment by extracting them from a note.

## Features

- **macOS Support:** Automatically retrieves a note from Apple Notes using AppleScript.
- **Linux/Other Support:** Falls back to reading a plain-text file (default: `$HOME/Notes.txt`).
- **Flexible Extraction:** Looks for lines starting with `export` between `<key_start>` and `</key_end>`.
- **Shell Compatibility:** Works in Bash and Zsh. (For Windows users, use Git Bash or WSL.)

## How It Works

1. **Retrieving the Note:**
   - On **macOS**, the script uses AppleScript (via `osascript`) to fetch the note content by title (default: `"API Keys"`).
   - On **Linux/Other**, it reads from a plain-text file (default: `$HOME/Notes.txt`).

2. **Cleaning the Content:**
   - Removes HTML tags (useful if AppleScript returns HTML).
   - Decodes HTML-encoded markers to get `<key_start>` and `</key_end>`.

3. **Extracting Exports:**
   - Extracts only the lines that begin with `export` (ignoring leading whitespace) found between `<key_start>` and `</key_end>`.

4. **Execution:**
   - Displays the cleaned content and export statements.
   - Prompts you for confirmation before executing the exports in your current shell.

## Installation

### 1. Save the Script

Save the script (provided in `add_api_key`) to your desired location.

### 2. Make It Executable

```bash
chmod +x /path/to/add_api_key
