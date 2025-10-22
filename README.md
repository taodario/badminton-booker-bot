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
