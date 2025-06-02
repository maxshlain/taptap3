# GitHub Copilot Instructions for TapTap3

## Project Overview

TapTap3 is a Python desktop application for macOS that solves multilingual typing problems. Users can continue typing in the wrong keyboard layout and double-tap Caps Lock to retroactively correct the text by switching languages and re-typing with proper character mapping.

## Core Functionality

- **Double Caps Lock Detection**: 500ms window for detecting double-tap
- **Character Buffer Management**: Tracks characters since last space (word boundary)
- **Language Switching**: Cycles through available languages (currently en ↔ ru)
- **Keyboard Simulation**: Deletes incorrect text and re-types with correct mapping

## Project Structure

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
```

## Technology Stack

- **Python 3.8+**: Main language
- **pynput**: Global keyboard listening and simulation
- **pytest**: Testing framework
- **macOS**: Target platform (requires Accessibility permissions)

## Code Style Guidelines

### Python Standards
- Follow PEP 8 guidelines
- Use type hints for all function parameters and return values
- Use descriptive variable and function names
- Maximum line length: 88 characters (Black formatter standard)

### Class and Method Patterns
- Use `@dataclass` for simple data containers
- Implement `__str__` and `__repr__` methods for debugging
- Use property decorators for computed attributes
- Handle exceptions gracefully with specific exception types

### Example Class Structure
```python
from dataclasses import dataclass
from typing import List, Optional
import time

@dataclass
class KeyboardEvent:
    key: str
    timestamp: float
    is_press: bool

class KeyboardHandler:
    def __init__(self, detection_window: float = 0.5):
        self.detection_window = detection_window
        self.character_buffer: List[str] = []
        self.caps_lock_presses: List[float] = []
    
    def handle_key_press(self, key: str) -> Optional[bool]:
        """Handle key press event. Returns True if language switch triggered."""
        # Implementation here
        pass
```

## Testing Patterns

### Mock External Dependencies
Always mock `pynput` components in tests:

```python
from unittest.mock import Mock, patch
import pytest

@patch('pynput.keyboard.Controller')
@patch('pynput.keyboard.Listener')
def test_keyboard_handler(mock_listener, mock_controller):
    # Test implementation
    pass
```

### Test Structure
- Use descriptive test method names: `test_double_caps_lock_triggers_language_switch`
- Test edge cases: timing boundaries, empty buffers, special characters
- Use fixtures for common test setup

## Key Implementation Details

### Timing Constraints
- Double Caps Lock detection window: 500ms
- Character buffer clears on space key
- Reset timing counters after successful detection

### Character Mapping (Future Implementation)
```python
# QWERTY to Cyrillic mapping example
QWERTY_TO_CYRILLIC = {
    'q': 'й', 'w': 'ц', 'e': 'у', 'r': 'к', 't': 'е',
    'y': 'н', 'u': 'г', 'i': 'ш', 'o': 'щ', 'p': 'з',
    # ... complete mapping
}
```

### Error Handling Patterns
```python
try:
    # Keyboard operations
    pass
except Exception as e:
    logger.error(f"Keyboard operation failed: {e}")
    # Graceful degradation
```

## macOS Specific Considerations

### Permissions
- Requires Accessibility permissions for global keyboard monitoring
- Use `pynput` permissions checking where available
- Provide clear error messages for permission issues

### System Integration
- Background service capability
- Respect system keyboard shortcuts
- Handle system sleep/wake events

## Development Priorities

### Current Focus (MVP)
1. Core double Caps Lock detection
2. Character buffer management
3. Basic language switching
4. Keyboard simulation (backspace + retype)

### Next Phase
1. Character mapping implementation (QWERTY ↔ Cyrillic)
2. System language detection
3. Configuration file support
4. Error handling and logging

### Future Enhancements
1. Multiple language support
2. Smart language detection
3. Custom key bindings
4. Menu bar integration

## Common Patterns to Use

### Event-Driven Architecture
```python
from typing import Callable

class EventEmitter:
    def __init__(self):
        self.callbacks: Dict[str, List[Callable]] = {}
    
    def on(self, event: str, callback: Callable):
        if event not in self.callbacks:
            self.callbacks[event] = []
        self.callbacks[event].append(callback)
    
    def emit(self, event: str, *args, **kwargs):
        for callback in self.callbacks.get(event, []):
            callback(*args, **kwargs)
```

### Configuration Management
```python
@dataclass
class Config:
    detection_window: float = 0.5
    languages: List[str] = None
    debug_mode: bool = False
    
    def __post_init__(self):
        if self.languages is None:
            self.languages = ["en", "ru"]
```

## Debugging Guidelines

### Logging Setup
```python
import logging

logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)
logger = logging.getLogger(__name__)
```

### Key Debugging Points
- Log all Caps Lock events with timestamps
- Track character buffer state changes
- Monitor language switching events
- Log keyboard simulation operations

## Security Considerations

- Minimize sensitive data in logs (avoid logging actual typed content)
- Handle keyboard input securely
- Respect user privacy with buffer management
- Clear sensitive data from memory when appropriate

## Performance Guidelines

- Keep keyboard event handlers lightweight
- Use efficient data structures for character buffers
- Minimize memory allocations in hot paths
- Consider async patterns for non-blocking operations

This project aims to provide seamless multilingual typing experience while maintaining system performance and user privacy.
