```markdown
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

Save the provided script (named `add_api_key`) to your desired location.

### 2. Make It Executable

```bash
chmod +x /path/to/add_api_key
```

### 3. Place It in Your PATH

For a system-wide installation on Unix-like systems (macOS, Linux), move it to `/usr/local/bin`:

```bash
sudo mv /path/to/add_api_key /usr/local/bin/
```

### 4. Source the Script for Shell Updates

Since the script uses `eval` to update environment variables, **you must source it**. To do so conveniently, add an alias to your shell configuration file:

- For **Bash** (add to `~/.bashrc`):

  ```bash
  echo "alias add_api_key='source /usr/local/bin/add_api_key'" >> ~/.bashrc
  source ~/.bashrc
  ```

- For **Zsh** (add to `~/.zshrc`):

  ```bash
  echo "alias add_api_key='source /usr/local/bin/add_api_key'" >> ~/.zshrc
  source ~/.zshrc
  ```

## Usage

Open a new terminal session and type:

```bash
add_api_key
```

The script will retrieve your note, clean its content, extract the export statements, prompt for confirmation, and then execute them so that the environment variables are set in your current shell.

## Configuration Options

You can override the default note title or fallback file path by setting the following environment variables before sourcing the script:

- `NOTE_TITLE`: The title of the note in Apple Notes (macOS).
- `NOTES_FILE`: The path to the plain-text file (Linux/Other).

Example:

```bash
export NOTE_TITLE="My API Keys"
export NOTES_FILE="$HOME/my_notes.txt"
source /usr/local/bin/add_api_key
```

## Compatibility

- **macOS:** Fully supported (AppleScript required).
- **Linux/Unix:** Supported via the fallback plain-text file.
- **Windows:** Run in a Unix-like environment (e.g., Git Bash or WSL).

## License

MIT

## Author
RubberDucky_AI
