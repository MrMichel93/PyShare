# PyShare Test Suite

## Overview
This test suite provides comprehensive automated and manual testing for the PyShare Python code editor. It validates all core functionality including syntax highlighting, code execution, linting, URL sharing, file operations, and UI interactions.

## Quick Start

### Running Automated Tests
1. **Open in browser**: Navigate to `tests.html`
2. **Click button**: Click "Run Automated Tests"
3. **Review results**: See pass/fail status for all 22 tests

**Auto-run mode**: `tests.html?autorun` - tests run automatically on page load

### Manual Testing
Refer to `TESTING.md` for detailed manual test cases and procedures.

## Test Coverage

### ✅ 22 Automated Tests (100% passing)

#### Python Syntax Highlighting (7 tests)
- Keywords highlighting (def, if, return, class, etc.)
- String highlighting (all quote types, f-strings, raw strings)
- Comment highlighting
- Number highlighting (int, float, hex, octal, binary)
- Function definition highlighting
- Class definition highlighting
- Built-in function highlighting

#### URL Sharing & Loading (4 tests)
- Content compression/decompression
- URL hash updates
- Content loading from hash
- URL length warning system

#### Save/Load Operations (2 tests)
- LocalStorage persistence
- Download functions (HTML, TXT, Python)

#### Output Console (2 tests)
- Console visibility
- Close button functionality

#### UI Elements (4 tests)
- Menu toggle
- Theme switching
- Menu item presence
- Editable article element

#### Editor Functionality (3 tests)
- Editor class initialization
- Content manipulation
- Parser availability

### 📋 Manual Tests

See `TESTING.md` for 40+ manual test cases covering:
- Cross-browser compatibility
- Responsive design
- Python code execution
- Linting functionality
- Edge cases and error handling

## Test Architecture

### Test Framework
- **Custom lightweight framework**: No external dependencies
- **Browser-based**: Runs entirely in the browser
- **Iframe isolation**: Each test runs in isolated iframe
- **Assertion helpers**: assertEquals, assertTrue, assertNotNull, etc.

### Test Structure
```javascript
runner.describe('Category Name', [
  {
    name: 'Test name',
    fn: async () => {
      // Test implementation
      const iframe = await loadIndexPage();
      // ... test logic ...
      assertTrue(condition, 'Error message');
    }
  }
]);
```

### Key Components
1. **TestRunner**: Manages test execution and results
2. **Assertion Helpers**: Validate test conditions
3. **Test Utilities**: Helper functions (loadIndexPage, sleep)
4. **Results Display**: Visual feedback with pass/fail indicators

## Test Files

```
PyShare/
├── tests.html          # Automated test suite (browser-based)
├── TESTING.md          # Manual test documentation
├── TEST_SUITE_README.md # This file
└── index.html          # Application under test
```

## Running Tests Locally

### Prerequisites
- Modern web browser (Chrome, Firefox, Safari, or Edge)
- Local web server (optional but recommended)

### With Web Server
```bash
# Python
python3 -m http.server 8080

# Node.js
npx http-server -p 8080

# Then open: http://localhost:8080/tests.html
```

### Without Web Server
Simply open `tests.html` in your browser directly. Some features may be limited due to CORS restrictions.

## Test Results Format

### Summary
```
✅ 22 Passed
❌ 0 Failed
📊 22 Total
⏱️ ~4000ms Duration
```

### Individual Results
Each test shows:
- ✓ or ✗ status indicator
- Test name
- Duration in milliseconds
- Error message (if failed)

## Understanding Test Failures

### Common Issues

**1. Syntax Highlighting Tests Fail**
- Cause: parsePython function not called correctly
- Fix: Ensure highlighting is triggered after content change

**2. URL Tests Fail**
- Cause: Compression/decompression not working
- Fix: Check browser compatibility with CompressionStream API

**3. UI Tests Fail**
- Cause: Elements not found or timing issues
- Fix: Increase sleep delays or check element selectors

**4. Editor Tests Fail**
- Cause: Editor initialization issues
- Fix: Verify Editor class is defined and instantiated

## Best Practices

### Writing New Tests
1. **Isolation**: Each test should be independent
2. **Cleanup**: Reset state between tests
3. **Timing**: Use appropriate delays for async operations
4. **Assertions**: Use descriptive error messages
5. **Focus**: Test one thing per test case

### Example Test
```javascript
{
  name: 'Highlights Python keywords correctly',
  fn: async () => {
    const iframe = await loadIndexPage();
    const doc = iframe.contentDocument;
    const win = iframe.contentWindow;
    const article = doc.querySelector('article');
    
    // Set content
    article.textContent = 'def hello():\n    return True';
    
    // Apply highlighting
    win.parsePython(article);
    
    // Wait for DOM update
    await sleep(50);
    
    // Assert
    const keywords = doc.querySelectorAll('.py-keyword');
    assertTrue(keywords.length > 0, 'Should have highlighted keywords');
  }
}
```

## Performance Considerations

### Test Execution Time
- Average: ~4 seconds for all 22 tests
- Each test: 100-300ms average
- Parallelization: Not implemented (sequential execution)

### Optimization Tips
- Reduce sleep delays where possible
- Reuse iframe instances when safe
- Minimize DOM queries
- Use efficient selectors

## Browser Compatibility

### Supported Browsers
- ✅ Chrome/Chromium (latest)
- ✅ Firefox (latest)
- ✅ Safari (latest)
- ✅ Edge (latest)

### Required APIs
- CompressionStream/DecompressionStream (for URL compression)
- localStorage
- querySelector/querySelectorAll
- Promise/async-await
- TextEncoder/TextDecoder

## Continuous Integration

### CI/CD Integration
The test suite can be integrated into CI pipelines:

```yaml
# Example GitHub Actions workflow
- name: Run Tests
  run: |
    npm install -g http-server
    http-server -p 8080 &
    npx playwright test tests.html
```

## Debugging Tests

### Browser DevTools
1. Open `tests.html` in browser
2. Open DevTools (F12)
3. Run tests
4. Check Console for errors
5. Use Network tab for CDN issues
6. Use Elements tab to inspect DOM

### Debug Mode
Add debug logging:
```javascript
console.log('Test state:', someVariable);
console.log('Element found:', element);
```

## Known Limitations

1. **Pyodide Loading**: Requires internet connection for CDN
2. **Code Execution**: Not tested in automated suite (requires Pyodide)
3. **File Operations**: Download tests verify function existence only
4. **Clipboard**: Cannot test clipboard API without user interaction
5. **Mobile**: Automated tests run in desktop mode only

## Contributing Tests

### Adding New Tests
1. Identify functionality to test
2. Write test following existing patterns
3. Add to appropriate test suite category
4. Run full test suite to verify
5. Update documentation

### Test Categories
- **Unit Tests**: Individual function testing
- **Integration Tests**: Feature testing
- **UI Tests**: User interface validation
- **E2E Tests**: End-to-end workflows (manual)

## Troubleshooting

### Tests Won't Run
- Check browser console for errors
- Verify `index.html` is accessible
- Check for CORS issues
- Try different browser

### Tests Fail Intermittently
- Increase sleep delays
- Check for race conditions
- Verify async operations complete
- Look for timing-dependent logic

### Tests Pass Locally, Fail in CI
- Check browser version differences
- Verify all dependencies available
- Check for environment-specific issues
- Review CI logs carefully

## Support

For issues or questions:
1. Check `TESTING.md` for manual test procedures
2. Review test code in `tests.html`
3. Check browser console for errors
4. Open GitHub issue with details

## Changelog

### v1.0.0 (Current)
- ✅ Initial test suite with 22 automated tests
- ✅ Comprehensive manual test documentation
- ✅ Browser-based test runner
- ✅ Visual results display
- ✅ 100% pass rate achieved

## Future Enhancements

### Planned Features
- [ ] E2E tests for Python execution
- [ ] Screenshot comparison tests
- [ ] Performance benchmarks
- [ ] Accessibility tests (ARIA, keyboard navigation)
- [ ] Mobile-specific interaction tests
- [ ] Automated cross-browser testing
- [ ] Code coverage reporting
- [ ] Visual regression testing

## License

Same as PyShare project.
