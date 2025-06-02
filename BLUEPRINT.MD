# taptap3 Application Summary

## Overview
taptap3 is a Python desktop application for macOS that solves the multilingual typing problem. Instead of manually switching keyboard layouts, users can continue typing and double-tap the Caps Lock key to retroactively correct text in the wrong language.

## Core Functionality
When a user double-taps Caps Lock:
1. The application deletes all characters typed since the last space
2. Switches to the next available keyboard language
3. Re-types the deleted characters using the correct language mapping

### Example Workflow
```
User types: "In russian, word hello is "ghbd"
User double-taps Caps Lock
Result: "In russian, word hello is "Прив"
```

## Architecture Overview

### Main Components

#### 1. Main Entry Point (`main.py`)
- Sets up global keyboard listeners using `pynput`
- Coordinates between keyboard handler and language switcher
- Manages application lifecycle

**Key responsibilities:**
- Initialize KeyboardHandler and LanguageSwitcher
- Set up global keyboard event listeners (press/release)
- Handle Caps Lock detection and trigger language switching

#### 2. Keyboard Handler (`keyboard_handler.py`)
- Tracks keyboard input and maintains character buffer
- Detects double Caps Lock taps within 500ms window
- Simulates backspace and re-typing functionality

**Key features:**
- Character buffer management (clears on space key)
- Caps Lock timing detection (0.5s window)
- Keyboard simulation via `pynput.Controller`

#### 3. Language Switcher (`language_switcher.py`)
- Manages available languages and current selection
- Cycles through languages (en → ru → en...)
- Provides language switching logic

**Current implementation:**
- Hardcoded languages: ["en", "ru"]
- Simple round-robin switching

## Technical Stack

### Dependencies
- **pynput**: Global keyboard listening and simulation
- **pytest**: Testing framework
- **Standard library**: time, unittest.mock

### Package Management
- Uses `pip` for dependency management
- Uses `uv` for Python version management
- No Poetry dependency

### Project Structure
```
src/
  taptap3/
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

## Implementation Details

### Caps Lock Detection Algorithm
1. Track timestamp of each Caps Lock press
2. If second press occurs within 500ms, increment counter
3. Reset counter if gap > 500ms
4. Trigger language switch when counter reaches 2

### Character Buffer Management
- Buffer stores characters typed since last space
- Space key clears the buffer (word boundary)
- Buffer is used for deletion and re-typing

### Language Switching Flow
1. Detect double Caps Lock
2. Simulate backspace for each character in buffer
3. Switch to next language
4. Re-type buffer characters (currently no translation)
5. Clear buffer and reset Caps Lock counter

## Testing Strategy

### Current Test Coverage
- **KeyboardHandler**: Caps Lock detection, buffer management, language switching
- **LanguageSwitcher**: Language cycling logic

### Test Approach
- Unit tests with mocking for hardware interactions
- Mock `pynput.Controller` for keyboard simulation testing
- Verify state management and timing logic

## Known Limitations & TODOs

### Current Limitations
1. **No character mapping**: Currently re-types original characters instead of translating
2. **Hardcoded languages**: Only English and Russian supported
3. **macOS only**: No cross-platform support
4. **No language detection**: Relies on manual switching

### Missing Features for Full Implementation
1. **Character mapping tables**: QWERTY → Cyrillic mapping
2. **System language detection**: Auto-detect available input sources
3. **Configuration**: User-configurable languages and timing
4. **Error handling**: Robust error handling for edge cases
5. **Accessibility**: macOS accessibility permissions handling

## Re-implementation Guide

### Step 1: Project Setup
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # macOS/Linux

# Install dependencies
pip install pynput pytest

# Create project structure
mkdir -p src/taptap3 tests
```

### Step 2: Core Components Implementation Order
1. **LanguageSwitcher**: Simple language cycling logic
2. **KeyboardHandler**: Input detection and buffering
3. **Character Mapping**: Add translation tables
4. **Main Application**: Tie components together
5. **System Integration**: macOS language detection

### Step 3: Essential Features
1. Global keyboard listening with pynput
2. Caps Lock double-tap detection (500ms window)
3. Character buffer management (word boundaries)
4. Keyboard simulation (backspace + retype)
5. Language cycling with proper character mapping

### Step 4: Advanced Features
1. System language source detection
2. User configuration file
3. Error handling and logging
4. Background service mode
5. Menu bar integration (macOS)

## Development Commands

### Running the Application
```bash
python -m src.taptap3.main
```

### Running Tests
```bash
pytest tests/
```

### Package Installation
```bash
pip install -e .
```

## macOS Specific Considerations

### Permissions Required
- **Accessibility**: Required for global keyboard listening
- **Input Monitoring**: Required for keystroke detection

### System Integration
- Background service capability
- Menu bar integration
- System language source detection via macOS APIs

## Future Enhancements
1. **Smart language detection**: AI-based language detection
2. **Custom mappings**: User-defined character mappings
3. **Multiple triggers**: Alternative trigger keys/combinations
4. **Cross-platform**: Windows and Linux support
5. **Cloud sync**: Settings synchronization across devices

This summary provides a complete blueprint for re-implementing taptap3 from scratch while understanding the current architecture and planned improvements.
