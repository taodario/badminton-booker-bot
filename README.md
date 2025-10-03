# Badminton Booker Bot 🏸

An automated booking bot for University of Toronto's badminton courts using Playwright for browser automation.

## Overview

This project automates the process of booking badminton courts at UofT's recreation facility. The bot handles login (including DUO authentication), navigates to the booking page, and attempts to book courts at specified times.

## Features

- **Automated Login**: Handles UofT authentication including DUO two-factor verification
- **Multiple Booking Strategies**:
  - `badmintonBookerCrude.py`: Single booking with precise timing
  - `badmintonBookerConstantCycle.py`: Continuous monitoring and booking across multiple dates/times
  - `nextDayBadmintonBookerConstantCycle.py`: Enhanced version with better error handling
- **Court Selection**: Attempts to book courts in priority order (Court 03 → Court 02 → Court 01)
- **Screenshot Capability**: Captures screenshots for debugging and verification
- **CAPTCHA Detection**: Identifies and handles reCAPTCHA challenges

## Prerequisites

- Python 3.7+
- Playwright
- UofT credentials with DUO authentication set up

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd badminton-booker-bot
```

2. Install required dependencies:
```bash
pip install playwright
playwright install chromium
```

3. Create a `config.py` file with your credentials:
```python
USERNAME = "your_utorid"
PASSWORD = "your_password"
```

⚠️ **Security Note**: Never commit your `config.py` file to version control. Add it to `.gitignore`.

## Usage

### Basic Booking (badmintonBookerCrude.py)

Interactive script that prompts for booking details:

```bash
python badmintonBookerCrude.py
```

You'll be asked to enter:
- Booking date (month, day, year)
- Desired time slot
- Refresh time (when to attempt booking)

### Constant Monitoring (badmintonBookerConstantCycle.py)

Continuously monitors and attempts to book specified dates and times:

```bash
python badmintonBookerConstantCycle.py
```

Edit the script to customize:
- `dates_to_consider`: List of dates to monitor
- `times_to_consider`: Time slots to book

### Next Day Booking (nextDayBadmintonBookerConstantCycle.py)

Similar to constant cycle but with improved error handling:

```bash
python nextDayBadmintonBookerConstantCycle.py
```

## Project Structure

```
badminton-booker-bot/
├── badmintonBookerCrude.py              # Basic interactive booking
├── badmintonBookerConstantCycle.py      # Continuous booking loop
├── nextDayBadmintonBookerConstantCycle.py  # Enhanced booking loop
├── config.py                            # Credentials (not in repo)
├── playwrightTutorial.py               # Playwright examples
├── screenshots/                         # Auto-generated screenshots
└── tests/                              # Test files
    ├── test_boilerplate_playwright.py
    ├── test_screenshot.py
    └── test_wait_until_time.py
```

## How It Works

1. **Login Flow**:
   - Navigates to UofT recreation website
   - Clicks sign-in and enters credentials
   - Waits for DUO verification (manual approval required)
   - Confirms browser trust

2. **Booking Flow**:
   - Navigates to S&R Badminton booking page
   - Selects specified date(s)
   - Iterates through courts in priority order
   - Attempts to click "Book Now" for desired time slots
   - Handles booking confirmation

3. **Error Handling**:
   - Takes screenshots on errors
   - Detects and handles CAPTCHA challenges
   - Implements retry logic with page refreshes

## Configuration Options

### Headless Mode

By default, the browser runs in headless mode. To see the browser in action:

```python
browser = chromium.launch(headless=False)
```

### Court Priority

Courts are attempted in this order:
1. Court 03-AC-Badminton
2. Court 02-AC-Badminton
3. Court 01-AC-Badminton

Modify the `courts` list in the script to change priorities.

### Timing Configuration

Adjust sleep intervals for different connection speeds:
```python
time_module.sleep(5)  # Adjust as needed
```

## Testing

Run tests using:
```bash
python -m pytest tests/
```

## Troubleshooting

### DUO Verification
- Ensure your phone is ready to approve DUO requests
- The script will pause and wait for manual approval

### CAPTCHA Issues
- The bot detects CAPTCHA challenges automatically
- Screenshots are saved to help diagnose issues
- Consider adjusting timing if CAPTCHAs appear frequently

### Booking Failures
- Check screenshots in the `screenshots/` directory
- Review console output for error messages
- Verify your credentials in `config.py`

## Disclaimer

This tool is for educational purposes. Please ensure you comply with:
- University of Toronto's Terms of Service
- Recreation facility booking policies
- Applicable automation and web scraping guidelines