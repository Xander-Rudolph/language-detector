# Language Detector GitHub Action

## Description
The **Language Detector** GitHub Action scans a repository for specific programming languages based on file extensions and returns the relative paths to directories where these languages are found. The results are provided as a JSON output.

## Features
- Automatically detects programming languages and their respective paths in the repository.
- Supports configurable working directory and recursion depth.
- Outputs results in a structured JSON format.
- Handles a wide range of programming languages and file types.

---

## Inputs

| Input Name    | Description                                | Required | Default Value |
|---------------|--------------------------------------------|----------|---------------|
| `working_dir` | Working path to execute the detection from | No       | `.` (current directory) |
| `fetch-depth` | Number of directory levels to scan         | No       | `1`           |

---

## Outputs

| Output Name      | Description                        |
|-------------------|------------------------------------|
| `languagePaths`   | JSON object of languages and paths |

---

## Usage

```yaml
name: Language Detection Workflow
on:
  push:
    branches:
      - main

jobs:
  detect-languages:
    runs-on: ubuntu-latest
    steps:
      - name: Use Language Detector
        uses: xander-rudolph/language-detector@v1
        with:
          working_dir: ./src
          fetch-depth: 2
      - name: Show Detected Languages
        run: |
          echo "Languages and their paths: ${{ steps.language-detection.outputs.languagePaths }}"
```

---

## Supported Languages

The action supports detecting paths for the following languages based on file extensions:

- **Web Development**: JavaScript (`.js`), TypeScript (`.ts`), HTML, CSS, JSON, YAML
- **Compiled Languages**: C, C++, C#, Java, Kotlin, Go, Swift, Rust
- **Scripting Languages**: Python, Ruby, PHP, Shell, PowerShell, Perl, Lua, R
- **Markup and Docs**: XML, Markdown, LaTeX
- **Functional Languages**: Haskell, Scala, Racket, Clojure, Erlang
- **Other**: Groovy, Dart, Fortran, Assembly, Batch, SQL, CoffeeScript, MATLAB, Objective-C++, Julia
- **Frameworks**: TypeScript JSX (`.tsx`), JavaScript JSX (`.jsx`)

---

## How It Works

1. **Repository Checkout**: The repository is checked out using the `actions/checkout@v4` action.
2. **Language Detection**: The script recursively scans files in the specified directory (default is the repository root) and matches file extensions to known languages.
3. **Output Generation**: The paths for each language are collected, deduplicated, and structured as a JSON object, which is set as the `languagePaths` output.

---

## Example Output

The `languagePaths` output will look something like this:

```json
{
  "JavaScript": ["./src/js", "./tests/js"],
  "Python": ["./src/python"],
  "Go": ["./src/go"],
  "Markdown": ["./docs"]
}
```

---

## Notes
- The action uses PowerShell for execution, ensuring compatibility with Windows and Linux runners.
- Results are deduplicated and sorted for clarity.
- You can modify the `fetch-depth` input to control how deeply the action scans directories.

---

## Contributions
Feel free to contribute by submitting issues or pull requests to enhance the action.

---

**License**: [MIT](LICENSE)  
**Author**: [Xander Rudolph](https://github.com/xander-rudolph)
