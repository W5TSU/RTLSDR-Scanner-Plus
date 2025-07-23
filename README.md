# RTLSDR Scanner #

A cross platform Python frequency scanning GUI for the OsmoSDR rtl-sdr.

## Updates in 2025

This update includes:

- **Code upgrade to Python 3** - Full compatibility with modern Python versions while maintaining backward compatibility
- **wxPython API updates** - Fixed deprecated method calls for current wxPython versions
- **matplotlib compatibility** - Updated for modern matplotlib versions
- **Enhanced stability** - Resolved numerous compatibility issues

This code seems to have rotted with time. The original website is gone. Remnants can be found on the [Wayback Machine](https://web.archive.org/web/*/http://eartoearoak.com/software/rtlsdr-scanner).

A basic [user manual](https://github.com/w5tsu/RTLSDR-Scanner-Plus/doc/Manual.md) is also available.

Tested on:

**Original Python 2.7 testing:**
- Windows 7 (x86 and x64)
- Windows 8.1 (x64)
- Ubuntu 12.04 (x86)
- Ubuntu 12.10 (x64)
- Ubuntu 13.04 (x64)
- Ubuntu 14.04 (x64)
- OS X Snow Leopard
- OS X Mountain Lion

**Current Python 3 testing (2025):**
- Ubuntu 22.04 (x64) with Python 3.10
- Modern Linux distributions with Python 3.6+

## Installation ##

### Python 3 Installation (Recommended)

**Prerequisites:**
- Python 3.6 or higher
- RTL-SDR drivers and libraries

**Install dependencies:**
```bash
pip3 install numpy matplotlib Pillow pyrtlsdr pyserial visvis wxpython
```

**Install RTLSDR Scanner:**
```bash
python3 setup.py develop --user
```

**Verify installation:**
```bash
python3 rtlsdr_scanner/rtlsdr_scan_diag.py
```

Windows executables for x86 and amd64 platforms are available on [GitHub](https://github.com/EarToEarOak/RTLSDR-Scanner/releases).

## Requirements ##

**Python 3 (Current):**
- [Python 3.6+](http://www.python.org)
- [wxPython](http://www.wxpython.org/)
- [matplotlib](http://matplotlib.org/)
- [numpy](http://www.numpy.org/)
- [Pillow](https://pypi.python.org/pypi/Pillow)
- [rtlsdr](http://sdr.osmocom.org/trac/wiki/rtl-sdr)
- [pyrtlsdr](https://github.com/roger-/pyrtlsdr)
- [pyserial](https://pypi.python.org/pypi/pyserial)

To test for missing libraries run:
```bash
python3 rtlsdr_scanner/rtlsdr_scan_diag.py
```

Windows 64 bit modules can be found [here](http://www.lfd.uci.edu/~gohlke/pythonlibs/)

## Usage ##

**GUI Mode:**
```bash
python3 -m rtlsdr_scanner [file]
```

**Command Line Mode:**
```bash
python3 -m rtlsdr_scanner -s <start_freq> -e <end_freq> [options] <output_file>
```

    file - optional saved scan file to load

**Command Line Options:**
- `-s START, --start START` - Start frequency (MHz)
- `-e END, --end END` - End frequency (MHz)
- `-w SWEEPS, --sweeps SWEEPS` - Number of sweeps
- `-p DELAY, --delay DELAY` - Delay between sweeps (s)
- `-g GAIN, --gain GAIN` - Gain (dB)
- `-d DWELL, --dwell DWELL` - Dwell time (seconds)
- `-f FFT, --fft FFT` - FFT bins
- `-l LO, --lo LO` - Local oscillator offset
- `-c CONF, --conf CONF` - Load a config file
- `-i INDEX, --index INDEX` - Device index (from 0)
- `-r REMOTE, --remote REMOTE` - Server IP and port

**Main Window**

- **Start** - Scan start frequency
- **Stop** - Scan stop frequency
- **Mode** - Single or continuous scanning
- **Dwell** - Sampling time spent on each step
- **FFT Size** - FFT size, greater values result in higher analysis precision (with higher sizes dwell should be increased)
- **Live update** - Update the display on each step (caution only use with small scans and low dwell times)
- **Grid** - Show a grid on the scan

**File Menu**

- **Open...** - Open a saved scan
- **Save As...** - Save a scan
- **Export...** - Export a scan to a CSV file
- **Properties..** - Scan information

**Edit Menu**

- **Preferences** - Set dongle gain, calibration, Local Oscillator and the sample bands to use

**Scan Menu**

- **Start** - Start a scan
- **Stop** - Stop a scan

**Tools Menu**

- **Compare** - Compare two previously saved scans
- **Auto Calibration** - Perform a crude calibration of the dongle to a known signal (this should be a continuous, steady signal)

## Troubleshooting ##

**Common Issues:**

- **Import Errors**: Ensure all dependencies are installed for Python 3
- **GUI Deprecation Warnings**: These are non-fatal and do not affect functionality
- **Drawing Artifacts**: Minor cosmetic issues may occur but core functionality works
- **RTL-SDR Not Found**: Ensure RTL-SDR drivers are properly installed

**Getting Help:**
- Check the diagnostics: `python3 rtlsdr_scanner/rtlsdr_scan_diag.py`
- Review the installation requirements above
- Ensure RTL-SDR hardware is properly connected and recognized

## License ##

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation version 3.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.


Copyright 2012 - 2015 Al Brown  
al [at] eartoearoak.com

Copyright 2025 Mark Grennan (W5TSU)  
mark [at] w5tsu.net

