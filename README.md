# [textarea.my](https://textarea.my)

A _minimalist_ Python code editor that lives entirely in your browser and stores everything in the URL hash.

<p align="center">
  <img src=".github/textarea-my-screenshot.webp" alt="Screenshot of textarea.my" width="696" height="456">
</p>

## Features

- 🐍 **Python Support** – Full Python syntax highlighting and execution
- 🗜️ **Compression** – Your code gets compressed with deflate
- 🔗 **URL hash** – Share your Python code by copying a URL
- ▶️ **Run Python** – Execute Python code directly in the browser with Pyodide
- 💾 **Save/Load** – Save as .py files or load Python scripts
- 💕 **Style** – Customize the look with CSS via DevTools

## Python-Specific Features

### 🎨 Syntax Highlighting

The editor provides comprehensive Python syntax highlighting for:

- **Keywords** – `def`, `class`, `if`, `for`, `while`, `import`, etc.
- **Built-in Functions** – `print()`, `len()`, `range()`, `open()`, etc.
- **Strings** – Single, double, triple-quoted, f-strings, and raw strings
- **Comments** – Line comments starting with `#`
- **Numbers** – Integers, floats, hex, octal, and binary literals
- **Decorators** – `@property`, `@staticmethod`, etc.
- **Function/Class Names** – Highlighted in function and class definitions

The syntax highlighting is theme-aware and adapts to both light and dark modes.

### ⚙️ Smart Editing Features

**Auto-indentation:**
- Press `Enter` after a colon (`:`) to automatically indent the next line by 4 spaces
- The editor maintains current indentation when creating new lines
- Follows Python's standard indentation conventions

**Auto-completion:**
- Press `Tab` to complete partial Python keywords and built-in functions
- Auto-closes brackets, parentheses, and quotes
- Skip over closing characters when typing

**Code Intelligence:**
- Real-time syntax checking as you type
- Visual error indicators for syntax issues
- Helpful error messages in the output console

## Running Python Code

### ▶️ How to Execute Code

1. Write or paste your Python code in the editor
2. Click the menu button (three dots) in the bottom-right corner
3. Select **"Run Python"** from the menu
4. View the output in the console that appears at the bottom

**Example:**
```python
# Simple Hello World
print("Hello, World!")

# Calculate factorial
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

print(f"Factorial of 5 is {factorial(5)}")
```

### 🔍 Output Console

- The output console displays print statements and execution results
- Error messages are shown in red for easy identification
- Click the × button to close the console
- The console automatically shows syntax errors as you type (after a brief delay)

### 🌐 Python Environment

- Powered by [Pyodide](https://pyodide.org/) – Python 3.11+ running in WebAssembly
- First run loads the Python environment (may take a few seconds)
- Subsequent runs execute instantly
- Supports most Python standard library modules
- No server required – everything runs locally in your browser

## URL Sharing Functionality

### 🔗 Share Your Python Code

The editor stores your code in the URL hash, making it incredibly easy to share:

1. Write your Python code
2. The URL automatically updates with your compressed code
3. Copy the URL and share it with anyone
4. Recipients can view, edit, and run your code instantly

**How it works:**
- Your code is compressed using deflate algorithm
- The compressed data is encoded in the URL hash
- When someone opens the URL, the code is automatically decompressed and displayed
- **No server storage** – your code travels with the URL

**URL Size Monitoring:**
- The menu shows current URL character count
- Warning (yellow) appears for URLs over 2,000 characters
- Error (red) appears for URLs over 8,000 characters (browser limit)
- URLs are safe to share across all modern browsers

**QR Code Support:**
- Add `/qr` to the URL to generate a QR code
- Perfect for sharing code with mobile devices
- Example: `https://textarea.my/qr#<your-compressed-code>`

## Saving and Loading Python Scripts

### 💾 Save Options

The editor provides multiple save formats:

**1. Save as Python (.py)**
- Click menu → **"Save as Python"**
- Downloads a `.py` file with your code
- Use the document title (if set with `# Title`) as filename
- Perfect for local development or sharing

**2. Save as TEXT (.txt)**
- Click menu → **"Save as TEXT"**
- Plain text format
- Useful for documentation or notes

**3. Save as HTML (.html)**
- Click menu → **"Save as HTML"** or press `Ctrl+S` / `Cmd+S`
- Saves a standalone HTML file with syntax highlighting
- No internet connection needed to view
- Perfect for archiving or offline viewing

### 📂 Load Python Files

**Loading a Python Script:**
1. Click menu → **"Load File"**
2. Select a `.py` file from your computer
3. The file contents replace the current editor content
4. Code is automatically syntax highlighted
5. URL is updated with the loaded code

**What happens when loading:**
- File is read locally (no upload to server)
- Content is displayed with Python syntax highlighting
- URL hash updates to reflect the new code
- Can immediately run, edit, or share

## Example Python Code to Test

Try these examples to explore the editor's capabilities:

### Example 1: Hello World
```python
# My First Python Program
print("Hello, World!")
print("Welcome to the PyShare editor!")
```

### Example 2: Data Structures
```python
# Working with lists and dictionaries
fruits = ["apple", "banana", "cherry"]
print("Fruits:", fruits)

person = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}
print(f"{person['name']} is {person['age']} years old")
```

### Example 3: Functions and Loops
```python
# Fibonacci sequence
def fibonacci(n):
    """Generate Fibonacci sequence up to n terms"""
    fib = [0, 1]
    for i in range(2, n):
        fib.append(fib[i-1] + fib[i-2])
    return fib[:n]

# Print first 10 Fibonacci numbers
result = fibonacci(10)
print("Fibonacci sequence:", result)
```

### Example 4: Classes and Objects
```python
# Object-oriented programming
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def bark(self):
        return f"{self.name} says Woof!"
    
    def description(self):
        return f"{self.name} is {self.age} years old"

# Create dog instances
buddy = Dog("Buddy", 3)
max_dog = Dog("Max", 5)

print(buddy.bark())
print(max_dog.description())
```

### Example 5: List Comprehensions
```python
# Advanced Python features
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Squares of even numbers
even_squares = [x**2 for x in numbers if x % 2 == 0]
print("Even squares:", even_squares)

# Dictionary comprehension
word_lengths = {word: len(word) for word in ["python", "code", "editor"]}
print("Word lengths:", word_lengths)
```

## Pro Tips

- Start your document with `# Title` to set a custom page title
- Your data lives in localStorage AND the URL. Double the fun!
- Add a `style` attribute to the `<article>` tag via DevTools. It'll be saved in the URL too!
- Add [`/qr`](https://textarea.my/qr#c0_NSy1KLElVSFQIDFJIzk9JVUjLL0ktVgQA) to get a QR code for the current page
- Press `Tab` for auto-completion of Python keywords
- Use `Enter` after `:` for automatic indentation
- The editor performs live syntax checking – errors appear in the output console

## Developer Documentation

### 🛠️ Contributing to PyShare

This section is for developers who want to modify or enhance the Python-specific features.

#### Architecture Overview

**Core Components:**

1. **Editor Engine** (`Editor` class in `index.html`)
   - Handles text editing, syntax highlighting, and cursor management
   - Uses contenteditable with custom parsing
   - Maintains undo/redo history

2. **Python Parser** (`parsePython` function)
   - Tokenizes Python code using regex patterns
   - Applies CSS classes for syntax highlighting
   - Supports keywords, strings, comments, numbers, decorators, etc.

3. **Python Execution** (Pyodide integration)
   - `initPyodide()` – Loads Pyodide runtime from CDN
   - `runPythonCode()` – Executes code and captures output
   - `lintPythonCode()` – Real-time syntax checking

4. **Storage & Compression**
   - `compress()` / `decompress()` – Deflate algorithm for URL encoding
   - `save()` / `load()` – LocalStorage and URL hash management

#### Modifying Python Syntax Highlighting

**Location:** `parsePython` function (around line 1042)

**To add new token types:**

```javascript
// 1. Define regex pattern
const myPattern = /pattern/y  // y flag for sticky matching

// 2. Add to matching loop
myPattern.lastIndex = i
res = myPattern.exec(input)
if (res && res.index === i) {
  const span = document.createElement('span')
  span.className = 'py-mytoken'  // CSS class
  span.textContent = res[0]
  frag.appendChild(span)
  i += res[0].length
  continue
}

// 3. Add CSS styling
.py-mytoken {
  color: #your-color;
}
```

**Token matching order matters:**
- Comments and strings are matched first (they can contain keywords)
- Decorators before keywords
- Function/class definitions before general keywords
- Specificity: most specific patterns should be tested first

#### Enhancing Python Execution

**Location:** `runPythonCode` and `initPyodide` functions (around line 1488)

**Adding Python packages:**

```javascript
async function installPackage(packageName) {
  const py = await initPyodide()
  await py.loadPackage(packageName)
}

// Usage in runPythonCode:
await installPackage('numpy')
await py.runPythonAsync(code)
```

**Custom Python environment setup:**

```javascript
async function initPyodide() {
  // ... existing initialization ...
  
  // Run Python setup code
  await pyodide.runPythonAsync(`
    import sys
    # Your custom initialization
  `)
  
  return pyodide
}
```

#### Modifying Auto-completion

**Location:** `handlePythonTyping` function (around line 1647)

**To add more keywords:**

```javascript
const pythonKeywords = [
  // Add your keywords here
  'match', 'case',  // Python 3.10+
  // Add more...
]
```

**To implement advanced completion:**

```javascript
// Example: complete from imported modules
const importedModules = ['os', 'sys', 'json']
// Add logic to track imports and suggest module methods
```

#### Improving Auto-indentation

**Location:** `handlePythonTyping` function, `Enter` key handler

**Current behavior:**
- Adds 4 spaces after `:` (colon)
- Maintains current indentation

**To enhance:**

```javascript
// Detect dedent scenarios (e.g., after pass, return, break)
if (currentLine.trim().match(/^(pass|return|break|continue)$/)) {
  // Reduce indentation
  const reducedIndent = currentIndent.slice(0, -4)
  document.execCommand('insertText', false, '\n' + reducedIndent)
  return
}
```

#### Extending Linting Features

**Location:** `lintPythonCode` function (around line 1540)

**Current implementation:**
- Uses Python's `ast.parse()` for syntax checking
- Shows errors in output console

**To add more checks:**

```javascript
const pythonCheckCode = `
import ast
import sys

try:
    tree = ast.parse(user_code)
    
    # Add custom checks
    for node in ast.walk(tree):
        # Example: warn about using 'eval'
        if isinstance(node, ast.Call):
            if isinstance(node.func, ast.Name) and node.func.id == 'eval':
                print("Warning: Using eval() can be dangerous", file=sys.stderr)
    
except SyntaxError as e:
    print(f"Syntax Error on line {e.lineno}: {e.msg}", file=sys.stderr)
`
```

#### File Structure

```
PyShare/
├── index.html          # Main application (HTML, CSS, JavaScript)
├── qr.html            # QR code generator page
├── tests.html         # Automated test suite
├── sw.js              # Service worker for PWA
├── manifest.json      # PWA manifest
├── README.md          # This file
├── TESTING.md         # Testing documentation
└── TEST_SUITE_README.md  # Test suite details
```

#### Testing Your Changes

**Manual Testing:**
1. Open `index.html` in a browser
2. Test your feature with various Python code samples
3. Check browser console for errors

**Automated Testing:**
1. Add tests to `tests.html`
2. Open `tests.html?autorun` to run tests
3. Verify all tests pass

**Test categories:**
- Syntax highlighting tests
- Code execution tests
- Save/load functionality tests
- URL compression tests
- Auto-completion tests

#### Code Style Guidelines

- Use ES6+ JavaScript features
- Prefer `const` over `let`, avoid `var`
- Use template literals for strings with variables
- Comment complex regex patterns
- Keep functions focused and small
- Use descriptive variable names

#### Pull Request Checklist

Before submitting a PR for Python features:

- [ ] Test syntax highlighting with various Python constructs
- [ ] Verify code execution works correctly
- [ ] Check URL compression with different code sizes
- [ ] Test save/load functionality
- [ ] Ensure auto-completion works as expected
- [ ] Verify auto-indentation behavior
- [ ] Run automated test suite (`tests.html`)
- [ ] Update documentation if adding new features
- [ ] Check browser compatibility (Chrome, Firefox, Safari, Edge)
- [ ] Test on mobile devices if UI changes made

#### Resources

- [Pyodide Documentation](https://pyodide.org/en/stable/) – Python in WebAssembly
- [Python Regex Reference](https://docs.python.org/3/library/re.html) – For syntax patterns
- [contenteditable Best Practices](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/contenteditable)
- [Compression Streams API](https://developer.mozilla.org/en-US/docs/Web/API/Compression_Streams_API)

#### Getting Help

- Open an issue on GitHub for bugs or feature requests
- Check existing issues and pull requests
- Review `TESTING.md` for testing guidelines
- Examine the code – it's well-structured and commented

---

*Made with ❤️ and JavaScript*
