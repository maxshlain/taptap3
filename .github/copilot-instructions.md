# GitHub Copilot Instructions for TapTap3

## Project Overview
TapTap3 is a Python macOS app that fixes multilingual typing. Double-tap Caps Lock to retroactively correct text by switching languages and re-typing with proper character mapping.

## Core Functionality
- **Double Caps Lock Detection**: 500ms window
- **Character Buffer**: Tracks characters since last space
- **Language Switching**: Cycles en ↔ ru
- **Keyboard Simulation**: Delete + retype with correct mapping

## Project Structure
```
src/
  main.py              # Entry point
  keyboard_handler.py  # Input handling & simulation
  language_switcher.py # Language management
tests/
  test_*.py           # Unit tests
```

## Technology Stack
- **Python 3.8+** with **pynput** for keyboard I/O
- **pytest** for testing
- **macOS** target (requires Accessibility permissions)

## Code Guidelines

### Style
- PEP 8, type hints, 88 char lines
- Use `@dataclass` for data containers
- Descriptive names, proper exception handling

### Key Patterns
```python
from dataclasses import dataclass
from typing import List, Optional

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
```

### Testing
Always mock `pynput`:
```python
@patch('pynput.keyboard.Controller')
@patch('pynput.keyboard.Listener')
def test_keyboard_handler(mock_listener, mock_controller):
    # Test implementation
```

## Core Implementation

### Timing
- 500ms double Caps Lock window
- Buffer clears on space
- Reset after successful detection

### Character Mapping
```python
QWERTY_TO_CYRILLIC = {
    'q': 'й', 'w': 'ц', 'e': 'у', 'r': 'к', 't': 'е',
    # ... complete mapping
}
```

### Error Handling
```python
try:
    # Keyboard operations
except Exception as e:
    logger.error(f"Operation failed: {e}")
    # Graceful degradation
```

## Development Priorities
1. **MVP**: Double Caps Lock detection, buffer management, basic switching
2. **Next**: Character mapping, system language detection, config
3. **Future**: Multi-language support, smart detection, menu bar

## Key Requirements
- Accessibility permissions for global keyboard monitoring
- Lightweight event handlers for performance
- Privacy-aware logging (no sensitive content)
- Background service capability
