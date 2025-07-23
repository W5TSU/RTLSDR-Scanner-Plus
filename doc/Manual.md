# RTLSDR Scanner Manual

**Wideband RF Spectrum Scanning**

*Originally compiled from PDF manual version dated 27/03/2017*

---

## Contents

- [Copyright and License](#copyright-and-license)
- [Introduction](#introduction)
- [Common Terms](#common-terms)
- [Graphical User Interface](#graphical-user-interface)
- [Command Line Interface](#command-line-interface)
- [Configuration File](#configuration-file)

---

## Copyright and License

### Copyright
- This document is Copyright © 2014 Al Brown
- The RTLSDR Scanner software is Copyright © 2012 – 2017 Al Brown

### License
Both this document and the RTLSDR Scanner software are licensed under the GNU General Public License version 3 (http://www.gnu.org/licenses/gpl.html).

### Contributors
Contributors to this document and the RTLSDR Scanner can be found at the GitHub page:
https://github.com/EarToEarOak/RTLSDR-Scanner/graphs/contributors

### Further Information
- **General information:** http://eartoearoak.com/software/rtlsdr-scanner
- **Installation instructions:** http://eartoearoak.com/software/rtlsdr-scanner/rtlsdr-scanner-installation
- **Code repository:** https://github.com/EarToEarOak/RTLSDR-Scanner

---

## Introduction

### What is RTLSDR Scanner?
RTLSDR Scanner is a wideband spectrum analyser for RTLSDR dongles which allows the visualisation of radio frequency signals.

The software is cross-platform and runs under Linux, Windows and OS X.

RTLSDR Scanner provides both GUI and command line interfaces.

### Required Hardware
- A PC, Mac or an embedded Linux platform such as the Raspberry Pi.
- A compatible RTLSDR dongle, see the OsmoSDR page for more details at http://sdr.osmocom.org/trac/wiki/rtl-sdr

### Installation
Installation of the RTLSDR driver and library dependencies are beyond the scope of this document, further details can be found at: http://eartoearoak.com/software/rtlsdr-scanner/rtlsdr-scanner-installation

> **Note for Python 3 users:** Use `python3 -m rtlsdr_scanner` instead of `python -m rtlsdr_scanner` in all examples.

---

## Common Terms

### Band Offset
The frequency offset where data is taken from to give a smooth scan and overcome the non-linear frequency response of the dongle.

### Dongle
The RTLSDR USB device to use to sample the radio data.

### Dwell
The time spent sampling at each frequency step, longer dwell times will slow the scanning speed but potentially reduce noise. For short-lived signals a fast dwell time should be used otherwise its amplitude may be significantly reduced.

### Frequency Calibration
The frequency compensation to apply to scanning to overcome errors in the dongle, specified in parts per million (ppm).

### FFT Size
The number of bins used for Fast Fourier Transform analysis, larger values give an increased frequency resolution but require more computational power and higher memory usage.

### Gain
The gain (amplification) specified in Decibels (dB) to set the dongle to during a scan.

### Geometric Mean
A type of mean (average) which indicates the typical value rather than the average value.

### Level Offset
The offset to be added to the signal to compensate for signal losses, specified in decibels (dB).

### Local Oscillator (LO)
The frequency offset to apply to scans if an external frequency converter (mixer) is used. Up and down converters are used to extend the tuning range to the dongle. For up-converters the offset is positive and negative for down-converters.

### Mean
The average.

### Resolution Bandwidth (RBW)
The minimum frequency between two separate peaks.

### Scan
One or more sweeps of the frequency range.

### Server
A dongle connected to a network which provides data via the rtl_tcp utility.

### Spectral Flatness
A measure of how flat the spectrum is. Pure white noise has a flatness of 1, this will decrease towards zero as more distinct signals appear above the noise floor.

### Sweep
A single pass of the frequency range.

### Power Spectral Density
The method for converting the radio data into a frequency spectrum.

### Window Function
A mathematical function used to reduce the effects of spectral leakage and noise when analysing data. Most users will probably want to leave this at its default (Hamming window).

---

## Graphical User Interface

### Main Window
The main window is split into 4 main areas: the Menu Bar, the Graph, the Measurement Table and Tool Bar.

### Menu Bar

#### File Menu
- **Open...** - Open a scan
- **Merge...** - Merge a scan with the current one
- **Backups...** - Restore a backup (enabled in the preferences window)
- **Recent Files...** - A list of recently used files
- **Save As...** - Save a scan
- **Export scan...** - Export a scan
- **Export image...** - Export an image
- **Export image sequence...** - Export sweeps as multiple images
- **Export map...** - Export a signal map
- **Export GPS track** - Export a GPX track log
- **Continuous Export…** - Export data at the end of each sweep
- **Properties...** - Properties of the current scan
- **Exit** - Exit the program

#### Edit Menu
- **Preferences...** - Show the preferences page
- **Advanced prefs...** - Advanced software settings
- **Number formatting...** - Adjust the precision of displayed numbers
- **Radio Devices...** - Radio settings
- **GPS...** - GPS settings

#### View Menu
- **Clear selection** - Clear a selection made by dragging with the middle mouse button
- **Show measurements** - Display the measurements table below the plot
- **Full screen** - Toggle full screen mode (F11)

#### Scan Menu
- **Start** - Start a scan
- **Continue** - Start and append sweeps to the current scan
- **Stop** - Immediately stop the scan
- **Stop at end** - Stop scanning at the end of the current sweep
- **Delay...** - Add a delay between sweeps

#### Tools Menu
- **Compare...** - Compare two scans
- **Smooth...** - Smooth the spectrum
- **Auto Calibration...** - Attempt to calibrate the dongle with a known frequency
- **Track in Google Earth** - Show scan locations in Google Earth
- **Track in Google Maps** - Display a heatmap of locations in a browser
- **GPS Satellites...** - Show the GPS signal strength if it's available

#### Help Menu
- **Help...** - Open up further information from the RTLSDR Scanner page
- **Check for updates...** - Check if an update is available
- **System information...** - Display details about the installation
- **About...** - Basic information about the program

### Graph
A plot of the scanned spectrum, three modes are currently available: Plot, Spectrogram and 3D Spectrogram.

A toolbar is available under the graph which allows panning and zooming in addition to plot specific commands.

The mouse wheel can be used to zoom 2 dimensional plots by first clicking the graph.

Further options are available by right-clicking the graph.

#### Standard Controls
- **Home** - Zoom to the default limits of the plot
- **Back** - Zoom to the previous view of the plot
- **Forward** - Zoom to the next plot view
- **Pan** - Pan the plot
- **Zoom** - Zoom to an area of the plot
- **Subplots** - Change the margins of the plot
- **Save** - Save the current plot as an image
- **Live update** - Update the plot as new data is processed (can be slow)
- **Grid** - Display a grid on the plot
- **Auto frequency** - Auto range the frequency axis to display all data
- **Auto level** - Auto range the level axis to display all data
- **Label peak** - Display a marker and label at the most recent peak
- **Smooth** - Smooth data display (right-click to change)
- **Differentiate** - Display the differentiated spectrum
- **Colour map** - The mapping of levels to colour

#### Plot Mode
A plot of the level versus frequency.

**Additional Controls:**
- **Multiple peaks** - Mark peaks above a threshold (right-click to change)
- **Fade plots** - Fade previous sweeps
- **Average plots** - Average all the sweeps
- **Minimum** - Plot the minimum of all sweeps
- **Maximum** - Plot the maximum of all sweeps
- **Variance** - Plot the variance of all sweeps
- **Delta** - Plot the delta from the first sweep

#### Spectrogram Mode
A plot of time versus frequency, level is displayed as colour. Often called a waterfall plot.

**Additional Controls:**
- **Auto time** - Auto range the time axis to display all data
- **Multiple peaks** - Mark peaks above a threshold (right-click to change)

#### 3D Spectrogram Mode
A three dimensional plot of frequency versus time versus level.

**Additional Controls:**
- **Auto time** - Auto range the time axis to display all data
- **Multiple peaks** - Mark peaks above a threshold (right-click to change)
- **Wireframe** - Plot the spectrum as a wireframe instead of colouring the faces

#### Other Display Modes
- **Status** - Displays the status of the current scan, often faster than the other plot types
- **Time Line** - Displays when sweeps occurred in time
- **Preview** - A fast preview plot (needs visvis)

### Measurement Table
To perform measurements of the spectrum use the middle mouse button to drag a selection box over the area of interest (in Plot or Spectrogram displays). You can also set the range by entering the values into the start and end cells in the table.

Measurements are taken from the last sweep.

### Tool Bar
The tool bar is used to control the main functions of the scanner.

- **Start** - Start a scan
- **Stop** - Immediately stop the scan
- **Range** - The frequency range
  - **Start** - The start frequency in megahertz
  - **Stop** - The end frequency in megahertz
- **Gain** - The dongle gain in Decibels
- **Mode** - Perform a single or multiple sweeps
  - **Single** - Only run a single sweep
  - **Continuous** - Run multiple sweeps until the scan is stopped
  - **Maximum** - Run until the maximum scans as defined in the preferences
- **Dwell** - The dwell time for each scanning step
- **FFT Size** - The number of FFT bins to calculate
- **Display** - The type of plot to display

### Properties Window
Displays the known properties of the scan. Latitude and longitude information may be edited here.

### Preferences Window
Allows generalised customisation of the software.

#### General Tab
- **Save warning** - Warn if a scan has not been saved before overwriting or exiting
- **Level alert** - Beep if the scan level is equal or greater than this level
- **Background colour** - The background colour of graph planes
- **Colour map** - The mapping to convert a level to colour in the view
- **Limit points** - The maximum number of points to plot

#### Continuous Scans Tab
Options pertaining to the continuous scan mode.
- **Average scans** - Average the current sweep with the previous one
- **Retain previous scans** - Keep previous sweeps
- **Max scans** - Maximum number of sweeps to keep

#### Plot View Tab
Settings related to the plot display
- **Fade previous scans** - Fade out older scans in the view
- **Line width** - Line width to use when plotting

### Advanced Preferences Window
Advanced settings.
- **PSD overlap** - Overlap percentage for power spectral density calculations
- **Window** - Change the window function used while scanning

### Radio Devices Window
A list of currently detected dongles and server settings.

- **Select** - Use this column to select a device to scan with
- **Device** - Displays the name of the dongle or the host and port of a server
- **Tuner** - The tuner type in the dongle
- **Serial Number** - The serial number of the dongle (not supported for servers)
- **Index** - The USB index of the dongle
- **Gain** - The gain to set the dongle to in Decibels
- **Frequency Calibration** - The frequency calibration to apply to the dongle in parts per million
- **Level Offset** - The level offset to be added to the signal
- **LO** - Local oscillator offset – used with frequency converters
- **Band offset...** - Click to open the band offset window
- **Add** - Add a server
- **Delete** - Delete the currently selected server

### GPS Window
Enabling GPS allows maps of signals to be built up, either NMEA or GPSd is supported.

The type can be set to:
- **GPSd** - A GPSd daemon
- **GPSd (Legacy)** - Older GPSd daemons
- **NMEA (Serial)** - NMEA serial connection
- **NMEA (Server)** - NMEA over TCP/IP

The host is a standard host name and optional port for NMEA (Server) and both GPSd options.

For NMEA (Serial), clicking the host allows the communication port settings to be changed.

Click the 'Test' entry to try the current settings.

### Window Function Window
Allows the setting of the window function that the scanner applies to incoming samples. This window is meant primarily for educational purposes as the default Hamming window gives the best results.

The first graph (green) displays how the window function tapers off data at the beginning and end of the sample to reduce leakage and noise when the sample is converted into frequency data.

The bottom graph (blue) displays the frequency response of the window function. The software takes data from the flattest sections of the graph ignoring the large peak which corresponds to 0Hz.

### Compare Window
Allows you to load two different scans and display the difference between them if their frequency bins coincide.

The first plot is shown in blue, the second in green and the difference in red.

### Auto Calibration Window
Basic calibration to a known signal.

Set the frequency and press calibrate, if you are happy with the result click OK.

Suitable signals are constant, unwavering signals such as that from a signal generator.

Real world sources such as FM radio transmissions can be used although the precision is reduced. In these cases it is recommended to set the dwell time to 1000ms to reduce errors.

### Band Offset Window
This window allows you to select the flattest part of the spectrum returned by the dongle, to improve the quality of the scan.

1. Disconnect the antenna from the dongle and ideally replace it with a 50 ohm load
2. Press refresh and wait for the spectrum to be displayed
3. Adjust the offset so the green bars cover the flattest section

---

## Command Line Interface

Scanning can be initiated from the command line.

### Format
```bash
python3 -m rtlsdr_scanner
    [-h]
    [-s START] [-e END]
    [-w SWEEPS] [-p DELAY]
    [-g GAIN] [-d DWELL] [-f FFT] [-l LO]
    [-c CONF]
    [-i INDEX | -r REMOTE]
    [file]
```

### Command Line Arguments

#### File
The file name to save the scan to, either ending in '.rfs' for native file or '.csv' to export to a comma separated values file.

#### Frequency Range
- `-s, --start` - Start of the frequency range in megahertz
- `-e, --end` - End of the frequency range in megahertz

#### Scan Parameters
- `-w, --sweeps` - Number of sweeps in a scan
- `-p, --delay` - Delay between sweeps in seconds
- `-g, --gain` - Scan gain in Decibels (optional, default: 0dB)
- `-d, --dwell` - Dwell time in seconds (optional, default: 131ms)
- `-f, --fft` - The number of FFT bins (optional, default: 1024)
- `-l, --lo` - The local oscillator offset in megahertz (optional, default: 0MHz)

#### Device Selection
- `-i, --index` - The zero-based index of the dongle (optional, cannot be used with -r)
- `-r, --remote` - The server host and port (optional, cannot be used with -i)

#### Configuration
- `-c, --config` - Path to a configuration file

#### Help
- `-h, --help` - Display help information

### Examples

**Scan from 88 to 108 MHz, saving to 'scan.rfs':**
```bash
python3 -m rtlsdr_scanner -s 88 -e 108 scan.rfs
```

**Scan from 430 to 436MHz, with a gain of 8.7dB and a dwell of 16ms, saving to 'test.rfs':**
```bash
python3 -m rtlsdr_scanner -s 430 -e 436 -g 8.7 -d 0.016 test.rfs
```

**Scanning using a second dongle:**
```bash
python3 -m rtlsdr_scanner -s 88 -e 108 -i 1 scan.rfs
```

**Scan using a server by name:**
```bash
python3 -m rtlsdr_scanner -s 88 -e 108 -r rtlserver:1234 scan.rfs
```

**Scan using a server by IP address:**
```bash
python3 -m rtlsdr_scanner -s 88 -e 108 -r 192.168.0.22:1234 scan.rfs
```

---

## Configuration File

When using the command line a configuration file can be loaded which specifies extra parameters. An example 'gps.conf' is included with the source.

### Format
The file consists of sections for each device, starting with a section header enclosed in square brackets and followed by a list of options. Multiple sections can be added but only the first one will be used.

The basic format is:
```ini
[section]
option1 = value
option2 = value
```

Where `section` is a unique name and `option` is one of the following:

### Required Options

#### Type
The GPS type:
- `0` - Serial
- `1` - GPSd
- `2` - GPSd (Legacy)
- `3` - NMEA (Server)

#### Resource
The serial port or IP address and port.

### Serial Options

#### Baud
The baud rate, defaults to 115200 (optional).

#### Bits
The number of data bits, defaults to 8 (optional).

#### Parity
The parity. N, E, O, M and S correspond to None, Even, Odd, Mark, Space respectively. Defaults to N (optional).

#### Stops
The number of stop bits, defaults to 1 (optional).

#### Soft
Enable software flow control, defaults to false (optional).

---

*This manual was converted from the original PDF format dated 27/03/2017 and updated for Python 3 compatibility.*