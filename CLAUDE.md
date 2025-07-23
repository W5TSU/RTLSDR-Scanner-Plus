# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

RTLSDR Scanner is a Python 3 cross-platform frequency scanning GUI for the OsmoSDR rtl-sdr library. Originally developed for Python 2.7, this codebase has been upgraded to Python 3 compatibility while maintaining backward compatibility where possible. It provides both GUI and command-line interfaces for spectrum analysis using RTL-SDR compatible USB devices.

**Recent Changes (2025):**
- Upgraded from Python 2.7 to Python 3 
- Fixed wxPython API compatibility issues
- Updated matplotlib compatibility
- Maintained backward compatibility with Python 2.7 where feasible

## Development Commands

### Running the Application

**GUI Mode:**
```bash
python3 -m rtlsdr_scanner
# Or with a saved scan file:
python3 -m rtlsdr_scanner [file]
```

**Command Line Mode:**
```bash
python3 -m rtlsdr_scanner -s <start_freq_mhz> -e <end_freq_mhz> <output_file>
```

**Library Diagnostics:**
```bash
python3 rtlsdr_scanner/rtlsdr_scan_diag.py
```

**Help:**
```bash
python3 -m rtlsdr_scanner --help
```

### Installation and Packaging

**Install in development mode:**
```bash
python3 setup.py develop --user
```

**Build distribution:**
```bash
python3 setup.py sdist
```

**Build Windows executable (using PyInstaller):**
```bash
pyinstaller pyinstaller.spec
```

## Python 2 to 3 Upgrade Notes

### Major Changes Applied

1. **Import Compatibility**: All Python 2 modules updated with try/except blocks for Python 3 compatibility:
   - `Queue` → `queue`
   - `ConfigParser` → `configparser`
   - `urlparse` → `urllib.parse`
   - `BaseHTTPServer` → `http.server`
   - `cPickle` → `pickle`

2. **Print Statements**: All `print "text"` converted to `print("text")`

3. **Dictionary Methods**: Updated deprecated iterator methods:
   - `.iteritems()` → `.items()`
   - `.itervalues()` → `.values()`
   - `.iterkeys()` → `.keys()`

4. **wxPython API Updates**: Fixed deprecated method calls:
   - `wx.PyControl` → `wx.Control`
   - `SetToolTipString()` → `SetToolTip()`
   - `AddCheckTool()` parameter updates

5. **Type Compatibility**: Fixed float/int type requirements for wx GUI elements

### Known Issues Post-Upgrade

- Some wxPython deprecation warnings (non-fatal)
- Minor drawing artifacts in custom widgets (functional but cosmetic)
- matplotlib navigation toolbar compatibility issues (navigation still works)

## Architecture

### Core Components

- **`main_window.py`**: Primary GUI application using wxPython with AUI (Advanced User Interface) panels
- **`cli.py`**: Command-line interface for headless scanning operations
- **`scan.py`**: Core scanning logic and spectrum processing
- **`devices.py`**: RTL-SDR device detection and management
- **`spectrum.py`**: Spectrum data structures and processing algorithms

### Key Modules

- **Plot modules** (`plot_*.py`): Various visualization components (3D, line plots, spectrograms, time plots)
- **Dialog modules** (`dialogs_*.py`): GUI dialog boxes for device setup, preferences, file operations
- **Utils modules** (`utils_*.py`): Utilities for matplotlib integration, wxPython helpers, and Google Maps integration

### Data Flow

1. Device detection via `get_devices_rtl()` in `devices.py`
2. Scan parameters configured through GUI (`main_window.py`) or CLI (`cli.py`)
3. Scanning performed by `ThreadScan` class in `scan.py`
4. Spectrum data processed and stored using classes in `spectrum.py`
5. Results displayed via plot modules or exported through `file.py`

## Dependencies

**Python 3 Dependencies:**
- wxPython (GUI framework)
- matplotlib (plotting)
- numpy (numerical processing)
- pyrtlsdr (RTL-SDR device interface)
- visvis (optional 3D visualization)
- Pillow (image processing)
- pyserial (serial communication)

**Development/Testing:**
- All dependencies are specified in `setup.py` and should be installed automatically

## File Formats

The application supports various scan file formats defined in `file.py`:
- Native binary format (.rfs)
- CSV export
- Image export (PNG, SVG)
- GPS coordinate export

## Configuration

- GPS configuration: `conf/gps.conf`
- Application settings managed through `settings.py`
- Device calibration and preferences stored in user config directories

## Development Notes

### Code Style
- Mixed Python 2/3 compatibility maintained using try/except blocks
- Original code style and structure preserved where possible
- New changes should follow existing patterns for consistency

### Testing
- Test GUI launch: `python3 -m rtlsdr_scanner` (should open without fatal errors)
- Test CLI: `python3 -m rtlsdr_scanner --help` (should show usage)
- Test diagnostics: `python3 rtlsdr_scanner/rtlsdr_scan_diag.py` (checks dependencies)

### Common Issues
- If encountering import errors, ensure all dependencies are installed for Python 3
- GUI may show deprecation warnings but should remain functional
- Some drawing operations may have minor cosmetic issues but core functionality works