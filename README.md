# TapTap3

> A Python desktop application for macOS that solves multilingual typing problems with intelligent keyboard layout switching.

## Overview

TapTap eliminates the hassle of manually switching keyboard layouts when typing in multiple languages. Simply continue typing and double-tap the Caps Lock key to retroactively correct text typed in the wrong language.

### How It Works

```
User types: "In russian, word hello is "ghbd"
User double-taps Caps Lock
Result: "In russian, word hello is "Прив"
```

When you double-tap Caps Lock, taptap:
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

# Start taptap3
python -m src.taptap3.main
```

### Basic Usage

1. Start typing in any application
2. When you notice you're typing in the wrong language, double-tap Caps Lock quickly (within 500ms)
3. The current word will be corrected automatically

### Supported Languages

Currently supported language pairs:
- English (QWERTY) ↔ Russian (Cyrillic)
