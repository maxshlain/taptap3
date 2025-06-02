# TapTap2

> A Python desktop application for macOS that solves multilingual typing problems with intelligent keyboard layout switching.

## Overview

TapTap2 eliminates the hassle of manually switching keyboard layouts when typing in multiple languages. Simply continue typing and double-tap the Caps Lock key to retroactively correct text typed in the wrong language.

### How It Works

```
User types: "In russian, word hello is "ghbd"
User double-taps Caps Lock
Result: "In russian, word hello is "Прив"
```

When you double-tap Caps Lock, TapTap2:
1. Deletes all characters typed since the last space
2. Switches to the next available keyboard language
3. Re-types the characters using the correct language mapping

## Features

- 🔄 **Automatic Language Switching**: Double-tap Caps Lock to switch languages retroactively
- ⌨️ **Smart Character Mapping**: Converts characters between keyboard layouts (e.g., QWERTY ↔ Cyrillic)
- 🎯 **Word-Boundary Detection**: Only corrects the current word (since last space)
- ⚡ **Fast Response**: 500ms detection window for double-tap
- 🖥️ **Global Hotkeys**: Works across all macOS applications

## Installation

### Prerequisites

- macOS (Monterey 12.0 or later recommended)
- Python 3.8+
- Accessibility permissions for keyboard monitoring

### Quick Install

```bash
# Clone the repository
git clone https://github.com/yourusername/taptap3.git
cd taptap3

# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Install the package
pip install -e .
```

### Setting Up Permissions

1. Go to **System Preferences** → **Security & Privacy** → **Privacy**
2. Select **Accessibility** from the left sidebar
3. Click the lock to make changes
4. Add your terminal application and Python to the list
5. Ensure both are checked

## Usage

### Running the Application

```bash
# Activate virtual environment
source venv/bin/activate

# Start TapTap2
python -m src.taptap2.main
```

### Basic Usage

1. Start typing in any application
2. When you notice you're typing in the wrong language, double-tap Caps Lock quickly (within 500ms)
3. The current word will be corrected automatically

### Supported Languages

Currently supported language pairs:
- English (QWERTY) ↔ Russian (Cyrillic)

## Development

### Project Structure

```
src/
  taptap2/
    __init__.py
    main.py              # Application entry point
    keyboard_handler.py  # Input handling and simulation
    language_switcher.py # Language management
tests/
  test_keyboard_handler.py
  test_language_switcher.py
requirements.txt
setup.py
```

### Architecture

- **Main Entry Point**: Coordinates global keyboard listeners and manages application lifecycle
- **Keyboard Handler**: Tracks input, detects double Caps Lock taps, and simulates keyboard actions
- **Language Switcher**: Manages available languages and switching logic

### Running Tests

```bash
# Run all tests
pytest tests/

# Run with coverage
pytest tests/ --cov=src/taptap2

# Run specific test file
pytest tests/test_keyboard_handler.py
```

### Development Setup

```bash
# Install development dependencies
pip install -r requirements-dev.txt

# Install pre-commit hooks
pre-commit install

# Run linting
flake8 src/ tests/

# Run type checking
mypy src/
```

## Technical Details

### Dependencies

- **pynput**: Global keyboard listening and simulation
- **pytest**: Testing framework
- **Standard library**: time, unittest.mock

### Caps Lock Detection Algorithm

1. Track timestamp of each Caps Lock press
2. If second press occurs within 500ms, increment counter
3. Reset counter if gap > 500ms
4. Trigger language switch when counter reaches 2

### Character Buffer Management

- Buffer stores characters typed since last space
- Space key clears the buffer (establishes word boundary)
- Buffer contents are used for deletion and re-typing

## Roadmap

### Current Limitations

- [ ] Character mapping not implemented (re-types original characters)
- [ ] Only English and Russian languages supported
- [ ] macOS only (no cross-platform support)
- [ ] No automatic language detection

### Planned Features

- [ ] **Character Mapping Tables**: Complete QWERTY ↔ Cyrillic translation
- [ ] **System Language Detection**: Auto-detect available input sources
- [ ] **User Configuration**: Customizable languages and timing settings
- [ ] **Cross-Platform Support**: Windows and Linux compatibility
- [ ] **Smart Language Detection**: AI-based language detection
- [ ] **Menu Bar Integration**: Native macOS menu bar interface

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Style

- Follow PEP 8 guidelines
- Use type hints where appropriate
- Write comprehensive tests for new features
- Update documentation for any API changes

## Troubleshooting

### Common Issues

**Application doesn't detect keystrokes:**
- Ensure Accessibility permissions are granted
- Check that Terminal/Python is in the Accessibility list
- Restart the application after granting permissions

**Double-tap not working:**
- Try adjusting typing speed (currently 500ms window)
- Ensure Caps Lock key is functioning properly
- Check for conflicting keyboard software

**Language switching not working:**
- Verify keyboard layouts are installed in System Preferences
- Check that target languages are available in macOS

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built with [pynput](https://pynput.readthedocs.io/) for cross-platform input handling
- Inspired by the need for seamless multilingual typing experiences

---

**Note**: This project is currently in development. Some features described in the roadmap are not yet implemented. See the [BLUEPRINT.md](BLUEPRINT.MD) for detailed technical specifications.