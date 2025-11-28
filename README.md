# iFix3r A12+ Activator

**Professional iOS Activation Bypass Tool**

---

[![Build](https://img.shields.io/badge/Build-Passing-brightgreen.svg)](https://github.com)
[![Platform](https://img.shields.io/badge/Platform-iOS%20A12%2B-blue.svg)](https://www.apple.com)
[![License](https://img.shields.io/badge/License-OSS-orange.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-1.0.0-lightgrey.svg)](https://github.com)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Screenshots](#-screenshots)
- [Installation](#-installation)
- [Requirements](#-requirements)
- [Quick Start](#-quick-start)
- [Project Structure](#-project-structure)
- [API Reference](#-api-reference)
- [Usage Guide](#-usage-guide)
- [Changelog](#-changelog)
- [Support](#-support)
- [Credits](#-credits)

---

## 🎯 Overview

**iFix3r A12+ Activator** is a professional-grade open-source tool designed to bypass iOS activation locks on A12 and newer Apple devices. The solution consists of a Python-based client application and a PHP-powered server backend that work together to generate and deploy device-specific activation payloads.

### What It Does

This tool automates the complex process of iOS activation bypass by:
- Automatically detecting device information and SystemGroup GUID
- Generating device-specific SQLite payload databases
- Deploying multi-stage activation payloads via AFC (Apple File Conduit)
- Supporting a wide range of iPhone and iPad models (A12+)

### Key Technologies

- **Client**: Python 3 with `pymobiledevice3` and `libimobiledevice`
- **Server**: PHP 7.4+ with SQLite3 and ZipArchive
- **Protocol**: AFC (Apple File Conduit) for file transfer
- **Database**: SQLite3 for payload generation

---

## ✨ Features

### Core Functionality

- ✅ **Automatic GUID Detection** - Scans device logs to extract SystemGroup GUID automatically
- ✅ **Manual GUID Input** - Fallback option for manual GUID entry with validation
- ✅ **Multi-Stage Payload Generation** - Three-stage activation process (fixedfile → BLDatabase → downloads.28)
- ✅ **Device-Specific Support** - Pre-configured plist files for 60+ device models
- ✅ **AFC File Transfer** - Supports both `ifuse` and `pymobiledevice3` for file deployment
- ✅ **Real-Time Validation** - Database integrity checks before deployment
- ✅ **Automated Cleanup** - Automatic removal of temporary files and old payloads

### Supported Devices

- **iPhone Models**: iPhone 11, 12, 13, 14, 15, 16, 17, 18 series
- **iPad Models**: iPad 8, 11, 12, 13, 14, 15 series
- **Architecture**: A12, A13, A14, A15, A16, A17, A18 chipsets

### Advanced Features

- 🔍 **Intelligent Log Scanning** - Binary tracev3 analysis for GUID extraction
- 📊 **Payload Pre-loading** - Pre-downloads all stages for faster deployment
- 🛡️ **Error Handling** - Comprehensive error detection and recovery
- 📝 **Detailed Logging** - Step-by-step progress reporting with colored output
- 🔄 **Automatic Fallback** - Graceful degradation between transfer methods

---

## 📸 Screenshots

### Client Interface
```
┌─────────────────────────────────────────┐
│  iOS Activation Tool - Professional    │
│                                         │
│  [✓] Verifying System Requirements...   │
│  [✓] Detecting Device...                │
│  Device: iPhone14,2 (iOS 17.0)          │
│  UDID: 00008030-001A...                 │
│                                         │
│  GUID Detection Options:                │
│  1. Auto-detect from device logs        │
│  2. Manual input                        │
└─────────────────────────────────────────┘
```

### Server Response
```json
{
  "success": true,
  "parameters": {
    "prd": "iPhone14,2",
    "guid": "2A22A82B-C342-444D-972F-5270FB5080DF",
    "sn": "F2LD..."
  },
  "links": {
    "step1_fixedfile": "https://...",
    "step2_bldatabase": "https://...",
    "step3_final": "https://..."
  }
}
```

---

## 🚀 Installation

### Prerequisites

Before installing, ensure you have the following:

- **Operating System**: Windows 10/11, macOS, or Linux
- **Python**: Version 3.8 or higher
- **PHP**: Version 7.4 or higher (for server)
- **Web Server**: Apache or Nginx (for server deployment)
- **iOS Device**: A12 or newer (iPhone/iPad)

### Client Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-repo/A12_Bypass_OSS.git
   cd A12_Bypass_OSS
   ```

2. **Install Python dependencies**
   ```bash
   pip3 install pymobiledevice3
   ```

3. **Install system dependencies**

   **On macOS:**
   ```bash
   brew install libimobiledevice
   brew install ifuse
   ```

   **On Linux (Ubuntu/Debian):**
   ```bash
   sudo apt-get update
   sudo apt-get install libimobiledevice6 libimobiledevice-utils ifuse
   ```

   **On Windows:**
   - Download `libimobiledevice` binaries from [official releases](https://github.com/libimobiledevice/libimobiledevice/releases)
   - Extract to a folder in your PATH

4. **Configure API endpoint**
   ```bash
   # Edit client/activator.py
   # Line 26: Update self.api_url with your server URL
   self.api_url = "https://your-domain.com/get2.php"
   ```

### Server Installation

1. **Upload server files**
   ```bash
   # Upload entire server/ directory to your web host
   scp -r server/* user@your-server:/var/www/html/
   ```

2. **Set permissions**
   ```bash
   chmod -R 755 /var/www/html/public
   chmod -R 777 /var/www/html/public/firststp
   chmod -R 777 /var/www/html/public/2ndd
   chmod -R 777 /var/www/html/public/last
   ```

3. **Configure web server**
   
   **Apache (.htaccess):**
   ```apache
   RewriteEngine On
   RewriteBase /
   ```

   **Nginx:**
   ```nginx
   location / {
       try_files $uri $uri/ /get2.php?$query_string;
   }
   ```

4. **Set up cron job** (optional, for cleanup)
   ```bash
   * * * * * php /var/www/html/cron/cleanup.php
   ```

---

## 📋 Requirements

### System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| **OS** | Windows 10 / macOS 10.14 / Ubuntu 18.04 | Latest version |
| **RAM** | 2 GB | 4 GB+ |
| **Storage** | 500 MB free space | 1 GB+ |
| **Network** | Internet connection | Stable broadband |

### Software Dependencies

#### Client Side
- **Python**: 3.8+
- **pymobiledevice3**: Latest version
- **libimobiledevice**: 1.3.0+
- **ifuse**: 1.1.3+ (optional, for macOS/Linux)
- **curl**: For HTTP requests

#### Server Side
- **PHP**: 7.4+ with extensions:
  - `sqlite3`
  - `zip`
  - `openssl`
  - `json`
- **Web Server**: Apache 2.4+ or Nginx 1.18+
- **SQLite**: 3.8+

### iOS Device Requirements

- **Device**: iPhone/iPad with A12 chip or newer
- **iOS Version**: iOS 14.0 or later
- **Connection**: USB cable (for initial setup)
- **Trust**: Device must trust the computer

---

## 🏃 Quick Start

### Running the Client

1. **Connect your iOS device** via USB
2. **Trust the computer** on your device when prompted
3. **Run the activator:**
   ```bash
   cd client
   python3 activator.py
   ```
4. **Follow the on-screen prompts:**
   - Choose GUID detection method (auto/manual)
   - Enter GUID if using manual mode
   - Wait for payload deployment
5. **Complete manual activation steps** as instructed

### Server Setup (Local Testing)

For local development, you can run a PHP development server:

```bash
cd server/public
php -S 0.0.0.0:8000
```

Then update the client's `api_url` to point to your local IP:
```python
self.api_url = "http://192.168.1.100:8000/get2.php"
```

---

## 📁 Project Structure

```
A12_Bypass_OSS/
│
├── client/                          # Python client application
│   ├── activator.py                # Main client script
│   └── README.md                   # Client documentation
│
├── server/                         # PHP server backend
│   ├── public/                    # Web-accessible files
│   │   ├── get.php                # Legacy endpoint
│   │   ├── get2.php               # Main API endpoint
│   │   ├── badfile.plist          # Template plist
│   │   ├── Maker/                 # Device-specific plist files
│   │   │   ├── iPhone11-2/
│   │   │   ├── iPhone12-1/
│   │   │   ├── iPhone13-1/
│   │   │   └── ... (60+ device folders)
│   │   ├── firststp/              # Stage 1 payloads (auto-generated)
│   │   ├── 2ndd/                   # Stage 2 payloads (auto-generated)
│   │   └── last/                    # Stage 3 payloads (auto-generated)
│   │
│   ├── cron/                       # Maintenance scripts
│   │   └── cleanup.php            # Automatic cleanup job
│   │
│   ├── templates/                  # SQL database templates
│   │   ├── bl_structure.sql       # BLDatabaseManager template
│   │   └── downloads_structure.sql # downloads.28 template
│   │
│   └── SETUP.md                   # Server setup guide
│
├── BLDatabaseManager.sql          # SQL dump (legacy)
├── BLDatabaseManager.sql2         # SQL dump (legacy)
├── downloads.28.sqlitedb          # Sample database
├── com.apple.MobileGestalt.plist  # Root plist template
│
└── README.md                      # This file
```

### Key Files Explained

- **`client/activator.py`**: Main Python script that handles device detection, GUID extraction, and payload deployment
- **`server/public/get2.php`**: PHP API endpoint that generates device-specific payloads
- **`server/public/Maker/`**: Directory containing device-specific `com.apple.MobileGestalt.plist` files
- **`server/templates/`**: SQL templates used to generate SQLite databases

---

## 🔌 API Reference

### Endpoint: `GET /get2.php`

Generates device-specific activation payloads.

#### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `prd` | string | Yes | Product type (e.g., `iPhone14,2`) |
| `guid` | string | Yes | SystemGroup GUID (UUID format) |
| `sn` | string | Yes | Device serial number |

#### Request Example

```bash
curl "https://your-domain.com/get2.php?prd=iPhone14,2&guid=2A22A82B-C342-444D-972F-5270FB5080DF&sn=F2LD12345678"
```

#### Response Format

```json
{
  "success": true,
  "parameters": {
    "prd": "iPhone14,2",
    "guid": "2A22A82B-C342-444D-972F-5270FB5080DF",
    "sn": "F2LD12345678"
  },
  "links": {
    "step1_fixedfile": "https://your-domain.com/firststp/abc123.../fixedfile",
    "step2_bldatabase": "https://your-domain.com/2ndd/def456.../belliloveu.png",
    "step3_final": "https://your-domain.com/last/ghi789.../apllefuckedhhh.png"
  },
  "debug": {
    "plist_used": "/path/to/plist",
    "plist_size": 1234
  }
}
```

#### Error Responses

```json
{
  "success": false,
  "error": "Missing prd, guid, or sn"
}
```

```json
{
  "success": false,
  "error": "Plist not found"
}
```

---

## 📖 Usage Guide

### Step 1: Device Detection

The client automatically detects your connected iOS device:

```bash
[✓] Detecting Device...
Device: iPhone14,2 (iOS 17.0)
UDID: 00008030-001A1D2E...
```

### Step 2: GUID Extraction

Choose between automatic or manual GUID detection:

**Automatic (Recommended):**
- Scans device logs for `BLDatabaseManager` references
- Extracts GUID from tracev3 binary data
- Validates GUID format and frequency

**Manual:**
- Enter GUID in format: `XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX`
- Input is validated before proceeding

### Step 3: Payload Generation

The server generates three payload stages:

1. **Stage 1 (fixedfile)**: EPUB-compliant ZIP containing device plist
2. **Stage 2 (belliloveu.png)**: BLDatabaseManager SQLite database
3. **Stage 3 (apllefuckedhhh.png)**: Final downloads.28.sqlitedb payload

### Step 4: Deployment

Payload is uploaded to device via AFC:

```
/Downloads/downloads.28.sqlitedb
```

### Step 5: Manual Activation

After deployment, follow these steps:

1. **Reboot device** (Settings → General → Shut Down)
2. **Check for iTunesMetadata.plist**:
   ```bash
   pymobiledevice3 afc pull /iTunes_Control/iTunes/iTunesMetadata.plist .
   ```
3. **Copy to Books directory**:
   ```bash
   pymobiledevice3 afc push iTunesMetadata.plist /Books/iTunesMetadata.plist
   ```
4. **Reboot again** to trigger bookassetd
5. **Monitor logs**:
   ```bash
   idevicesyslog | grep -E 'itunesstored|bookassetd'
   ```

---

## 📝 Changelog

### Version 1.0.0 (2024)

#### Added
- Initial release of A12+ activation bypass tool
- Automatic GUID detection from device logs
- Support for 60+ iPhone and iPad models
- Multi-stage payload generation system
- PHP server backend with SQLite database generation
- Python client with AFC file transfer
- Comprehensive error handling and logging
- Automated cleanup scripts

#### Features
- ✅ Auto-detect SystemGroup GUID from tracev3 logs
- ✅ Manual GUID input with validation
- ✅ Device-specific plist file support
- ✅ Three-stage payload deployment
- ✅ ifuse and pymobiledevice3 transfer methods
- ✅ Real-time progress reporting
- ✅ Database integrity validation

#### Technical Details
- Client: Python 3.8+ with pymobiledevice3
- Server: PHP 7.4+ with SQLite3
- Protocol: AFC (Apple File Conduit)
- Database: SQLite3 with custom schemas

---

## 💬 Support

### Getting Help

- **Documentation**: Check the `client/README.md` and `server/SETUP.md` files
- **Issues**: Report bugs or request features via GitHub Issues
- **Community**: Join our Discord server (link placeholder)

### Common Issues

**Problem**: Device not detected
- **Solution**: Ensure device is trusted and USB debugging is enabled

**Problem**: GUID not found automatically
- **Solution**: Use manual input mode with GUID from device logs

**Problem**: Server returns "Plist not found"
- **Solution**: Verify device model is supported in `server/public/Maker/`

**Problem**: AFC transfer fails
- **Solution**: Try switching between ifuse and pymobiledevice3 modes

### Contact Information

- **Website**: [https://hasnit3ch.com](https://hasnit3ch.com) (placeholder)
- **Email**: support@hasnit3ch.com (placeholder)
- **GitHub**: [https://github.com/hasnit3ch](https://github.com/hasnit3ch) (placeholder)

---

## 🙏 Credits

### Development Team

**HASNIT3CH SOLUTION**  
*Professional iOS Security Research & Development*

**iFix3r A12+ Activator**  
*Open Source Activation Bypass Tool*

### Contributors

- **HASNIT3CH** - Project Lead & Core Development
- **iFix3r Team** - Testing & Device Support

### Acknowledgments

- **libimobiledevice** - iOS device communication library
- **pymobiledevice3** - Python iOS device interface
- **Apple** - iOS platform (for research purposes)

### License

This project is released as open-source software. Please refer to the LICENSE file for details.

---

## 📄 License

This project is provided as-is for educational and research purposes. Use at your own risk.

---

## 🔗 Links

- **Download**: [Latest Release](https://github.com/your-repo/releases) (placeholder)
- **Documentation**: [Full Documentation](https://docs.hasnit3ch.com) (placeholder)
- **Support**: [Discord Community](https://discord.gg/hasnit3ch) (placeholder)

---

<div align="center">

**Made with ❤️ by HASNIT3CH SOLUTION**

*Professional iOS Security Tools*

[![HASNIT3CH](https://img.shields.io/badge/HASNIT3CH-SOLUTION-red.svg)](https://hasnit3ch.com)
[![iFix3r](https://img.shields.io/badge/iFix3r-A12%2B%20Activator-blue.svg)](https://ifix3r.com)

© 2024 HASNIT3CH SOLUTION. All rights reserved.

</div>

