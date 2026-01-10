# PyShare Testing Documentation

This document provides comprehensive testing guidelines for the PyShare Python code editor.

## Table of Contents
1. [Running Automated Tests](#running-automated-tests)
2. [Manual Test Cases](#manual-test-cases)
3. [Test Coverage](#test-coverage)
4. [Known Issues](#known-issues)

## Running Automated Tests

### Prerequisites
- A modern web browser (Chrome, Firefox, Safari, or Edge)
- Local web server (or open `tests.html` directly)

### Running Tests
1. Open `tests.html` in your web browser
2. Click the "Run Automated Tests" button
3. Wait for all tests to complete
4. Review the test results

Alternatively, for automated test runs, append `?autorun` to the URL:
```
file:///path/to/PyShare/tests.html?autorun
```

## Manual Test Cases

### 1. Python Syntax Highlighting

#### Test Case 1.1: Keyword Highlighting
**Steps:**
1. Open `index.html`
2. Type: `def hello():`
3. Observe the syntax highlighting

**Expected Result:**
- `def` should be highlighted in keyword color (red/pink)
- Function name should be highlighted in function color (purple)

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 1.2: String Highlighting
**Steps:**
1. Type: `message = "Hello World"`
2. Observe highlighting

**Expected Result:**
- String `"Hello World"` should be highlighted in string color (green/blue)

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 1.3: Comment Highlighting
**Steps:**
1. Type: `# This is a comment`
2. Observe highlighting

**Expected Result:**
- Comment should be in gray/muted color and italic

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 1.4: Number Highlighting
**Steps:**
1. Type: `x = 42` and `y = 3.14`
2. Observe highlighting

**Expected Result:**
- Numbers should be highlighted in number color (blue)

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 1.5: Complex Code Highlighting
**Steps:**
1. Type or paste the following code:
```python
class Calculator:
    def add(self, a, b):
        return a + b
    
    def multiply(self, x, y):
        # Multiply two numbers
        result = x * y
        return result

calc = Calculator()
print(calc.add(5, 3))
```
2. Verify all elements are correctly highlighted

**Expected Result:**
- `class`, `def`, `return` are highlighted as keywords
- `Calculator`, `add`, `multiply` are highlighted appropriately
- Comments are in gray italic
- Numbers are in blue
- Strings are in green/blue

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

### 2. Code Execution (Browser-based)

#### Test Case 2.1: Simple Print Statement
**Steps:**
1. Type: `print("Hello, World!")`
2. Click menu button (three dots)
3. Click "Run Python"
4. Wait for Pyodide to load
5. Observe output console

**Expected Result:**
- Output console appears at bottom
- Shows: `Hello, World!`
- No errors displayed

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 2.2: Mathematical Operations
**Steps:**
1. Type:
```python
x = 10
y = 20
result = x + y
print(f"Result: {result}")
```
2. Run Python
3. Observe output

**Expected Result:**
- Output shows: `Result: 30`

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 2.3: Loop Execution
**Steps:**
1. Type:
```python
for i in range(5):
    print(i)
```
2. Run Python
3. Observe output

**Expected Result:**
- Output shows numbers 0-4 on separate lines

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 2.4: Error Handling
**Steps:**
1. Type: `print(undefined_variable)`
2. Run Python
3. Observe output

**Expected Result:**
- Output console shows error in red
- Error message mentions `NameError` or similar

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 2.5: Function Definition and Call
**Steps:**
1. Type:
```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

for i in range(10):
    print(fibonacci(i), end=' ')
```
2. Run Python
3. Observe output

**Expected Result:**
- Output shows Fibonacci sequence: `0 1 1 2 3 5 8 13 21 34`

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

### 3. Linting Tool Integration

#### Test Case 3.1: Syntax Error Detection
**Steps:**
1. Type: `def hello(` (incomplete syntax)
2. Wait 1-2 seconds
3. Observe output console

**Expected Result:**
- Output console appears automatically
- Shows syntax error message in red
- Indicates the line number of error

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 3.2: Valid Code - No Errors
**Steps:**
1. Type: `def hello():\n    return "Hi"`
2. Wait 1-2 seconds
3. Observe behavior

**Expected Result:**
- No error messages appear
- Output console closes or shows no errors

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 3.3: Indentation Error
**Steps:**
1. Type:
```python
def test():
print("wrong indent")
```
2. Wait for linting
3. Observe output

**Expected Result:**
- Syntax error about indentation is displayed

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

### 4. URL Sharing and Loading Functionality

#### Test Case 4.1: Content Compression
**Steps:**
1. Type a simple Python script
2. Observe the URL in the address bar
3. Note the hash portion after `#`

**Expected Result:**
- URL contains a hash with compressed content
- Hash is base64url encoded

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 4.2: Share and Load
**Steps:**
1. Type: `print("Test sharing")`
2. Wait for URL to update
3. Copy the full URL
4. Open a new browser tab/window
5. Paste the URL and press Enter
6. Observe the editor content

**Expected Result:**
- New tab/window loads the same content
- Code is properly displayed
- Syntax highlighting is applied

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 4.3: Long Content Warning
**Steps:**
1. Create or paste a very long Python script (>2000 characters)
2. Observe notifications and URL size indicator

**Expected Result:**
- URL size indicator in menu shows character count
- Warning notification appears (orange) for large content
- Error notification (red) for very large content (>8000 chars)

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 4.4: Empty Hash Handling
**Steps:**
1. Open `index.html` with no hash
2. Observe initial state

**Expected Result:**
- Editor loads with empty content or localStorage content
- No errors in console

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 4.5: Invalid Hash Handling
**Steps:**
1. Open `index.html#invalidhashcontent`
2. Observe behavior

**Expected Result:**
- Editor loads with empty content
- No crashes or errors
- Application remains functional

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

### 5. Output Console Accuracy and Error Reporting

#### Test Case 5.1: Standard Output
**Steps:**
1. Type: `print("Line 1")\nprint("Line 2")`
2. Run code
3. Observe output console

**Expected Result:**
- Both lines appear in output console
- Correct order maintained

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 5.2: Error Output
**Steps:**
1. Type: `1 / 0`
2. Run code
3. Observe output

**Expected Result:**
- Error message in red
- Shows `ZeroDivisionError` or similar
- Includes traceback information

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 5.3: Mixed Output and Errors
**Steps:**
1. Type:
```python
print("Before error")
raise ValueError("Test error")
print("After error")
```
2. Run code
3. Observe output

**Expected Result:**
- "Before error" appears first
- Error message appears in red
- "After error" does not appear

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 5.4: Console Close Button
**Steps:**
1. Run any code to show output
2. Click the × button on output console
3. Observe behavior

**Expected Result:**
- Output console closes/hides
- Can be reopened by running code again

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

### 6. Save/Load Operations for .py Files

#### Test Case 6.1: Save as Python File
**Steps:**
1. Type a Python script
2. Click menu button
3. Click "Save as Python"
4. Choose save location
5. Verify file is downloaded

**Expected Result:**
- File downloads with `.py` extension
- File contains the exact code from editor
- Filename includes document title if set

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 6.2: Load Python File
**Steps:**
1. Click menu button
2. Click "Load File"
3. Select a `.py` file from your computer
4. Observe editor content

**Expected Result:**
- File content loads into editor
- Syntax highlighting is applied
- Previous content is replaced
- Success notification appears

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 6.3: Save as HTML
**Steps:**
1. Type content with title: `# My Document`
2. Click "Save as HTML"
3. Verify downloaded file

**Expected Result:**
- HTML file downloads
- Contains styled content
- Opens properly in browser

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 6.4: Save as TEXT
**Steps:**
1. Type any content
2. Click "Save as TEXT"
3. Verify downloaded file

**Expected Result:**
- Plain text file downloads
- Contains raw content without styling

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

### 7. Responsiveness and Cross-Browser Functionality

#### Test Case 7.1: Desktop Responsive (1920x1080)
**Steps:**
1. Open in browser at full screen (1920x1080)
2. Verify all UI elements are visible
3. Test all features

**Expected Result:**
- All elements properly positioned
- Text is readable
- No overflow or clipping

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 7.2: Desktop Responsive (1366x768)
**Steps:**
1. Resize browser to 1366x768
2. Verify layout
3. Test features

**Expected Result:**
- Layout adapts properly
- Menu is accessible
- Content area is usable

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 7.3: Tablet View (iPad)
**Steps:**
1. Open on iPad or use browser device emulation
2. Test in portrait and landscape
3. Verify all features work

**Expected Result:**
- Layout is responsive
- Touch interactions work
- Menu is accessible
- Virtual keyboard doesn't break layout

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 7.4: Mobile View (iPhone)
**Steps:**
1. Open on iPhone or use device emulation
2. Test in portrait orientation
3. Verify features

**Expected Result:**
- Content is readable without zooming
- Menu button is accessible
- Floating action button doesn't overlap content
- Virtual keyboard works properly

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 7.5: Chrome Browser
**Steps:**
1. Open application in latest Chrome
2. Test all features
3. Check console for errors

**Expected Result:**
- All features work correctly
- No console errors
- Smooth performance

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 7.6: Firefox Browser
**Steps:**
1. Open application in latest Firefox
2. Test all features
3. Check console for errors

**Expected Result:**
- All features work correctly
- No console errors
- Syntax highlighting works
- Code execution works

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 7.7: Safari Browser
**Steps:**
1. Open application in latest Safari
2. Test all features
3. Check console for errors

**Expected Result:**
- All features work correctly
- No console errors
- Compression/decompression works
- File operations work

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 7.8: Edge Browser
**Steps:**
1. Open application in latest Edge
2. Test all features
3. Check console for errors

**Expected Result:**
- All features work correctly
- No console errors
- All APIs supported

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

### 8. Additional Features

#### Test Case 8.1: Theme Toggle
**Steps:**
1. Click menu button
2. Click "Dark Theme" or "Light Theme"
3. Observe changes

**Expected Result:**
- Theme switches between light and dark
- Syntax colors adjust appropriately
- Preference is saved in localStorage

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 8.2: QR Code Generation
**Steps:**
1. Type some content
2. Click menu button
3. Click "Generate QR code"
4. Observe QR code page

**Expected Result:**
- QR code page loads
- QR code is visible
- Scanning QR code loads the content

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 8.3: Share Document (Copy Link)
**Steps:**
1. Type content
2. Click menu button
3. Click "Share document"
4. Observe notification

**Expected Result:**
- Link copied to clipboard
- Success notification appears
- Pasted link loads the content

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 8.4: New Document
**Steps:**
1. Click menu button
2. Click "New document"
3. Observe behavior

**Expected Result:**
- Opens in new tab/window
- Editor is empty
- All features work

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 8.5: Keyboard Shortcuts
**Steps:**
1. Type content
2. Press Ctrl+S (or Cmd+S on Mac)
3. Observe behavior

**Expected Result:**
- Save as HTML is triggered
- File downloads

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 8.6: Auto-indent on Enter after Colon
**Steps:**
1. Type: `def test():`
2. Press Enter
3. Observe cursor position

**Expected Result:**
- Cursor is indented by 4 spaces on new line

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 8.7: Tab Key for Indentation
**Steps:**
1. Type some code
2. Press Tab
3. Observe behavior

**Expected Result:**
- Inserts 4 spaces (Python standard)
- OR completes keyword if partial word typed

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

#### Test Case 8.8: Auto-closing Brackets
**Steps:**
1. Type: `(`
2. Observe behavior

**Expected Result:**
- Automatically adds closing `)`
- Cursor positioned between brackets

**Status:** ⬜ Not Tested | ✅ Pass | ❌ Fail

## Test Coverage

### Automated Tests
- ✅ Python syntax highlighting (keywords, strings, comments, numbers, functions, classes, builtins)
- ✅ URL compression and decompression
- ✅ URL hash updates
- ✅ Content loading from hash
- ✅ URL length warnings
- ✅ LocalStorage save operations
- ✅ Download function existence
- ✅ Output console visibility
- ✅ Output console close functionality
- ✅ Menu toggle functionality
- ✅ Theme toggle functionality
- ✅ UI element presence
- ✅ Editor initialization
- ✅ Editor content manipulation

### Manual Tests Required
- ⬜ Code execution accuracy (requires Pyodide)
- ⬜ Cross-browser compatibility
- ⬜ Responsive design on actual devices
- ⬜ File upload/download functionality
- ⬜ Clipboard operations
- ⬜ QR code generation
- ⬜ Service worker offline functionality
- ⬜ Performance with large files
- ⬜ Keyboard shortcuts

## Known Issues

### Issues to Monitor
1. **Pyodide Loading Time**: First-time Python execution may take several seconds to load Pyodide library
2. **URL Length Limits**: Browsers have varying URL length limits (typically 2000-8000 characters)
3. **Large File Performance**: Very large Python files may cause performance issues in syntax highlighting
4. **Mobile Keyboard**: Virtual keyboard may overlap content on some mobile devices

### Browser-Specific Issues
- **Safari**: File System Access API may not be fully supported (affects save dialogs)
- **Mobile Safari**: Clipboard API may require user interaction
- **Firefox**: Some compression APIs may require feature flags in older versions

## Testing Checklist

Before releasing a new version, ensure:
- [ ] All automated tests pass
- [ ] Manual tests completed on at least 2 browsers
- [ ] Mobile responsiveness verified
- [ ] No console errors in any browser
- [ ] Python execution works correctly
- [ ] URL sharing works correctly
- [ ] File operations work correctly
- [ ] Syntax highlighting works for various Python code samples
- [ ] Error handling works properly
- [ ] Performance is acceptable for typical use cases

## Reporting Issues

When reporting issues, please include:
1. Browser name and version
2. Operating system
3. Steps to reproduce
4. Expected behavior
5. Actual behavior
6. Console errors (if any)
7. Screenshots (if applicable)

## Contributing Tests

To add new tests:
1. Open `tests.html`
2. Add test cases to appropriate test suite using `runner.describe()`
3. Use assertion helpers: `assert()`, `assertEquals()`, `assertTrue()`, etc.
4. Test your tests by running the full suite
5. Update this documentation with new manual test cases
