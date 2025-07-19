Prank Server

WARNING: This software is designed purely for harmless pranks on consenting parties. Use responsibly and at your own risk. By using this software, you acknowledge that you are solely responsible for any consequences that arise from its use.

Description

A lightweight, stealthy prank server that listens for remote commands to trigger a variety of harmless pranks on a target Windows PC. Commands include simulating key presses (e.g., Alt+F4), mouse jiggling, random pop-ups, volume adjustments, network spikes, and more.

Features

Remote Control Menu: Send commands from a client script to trigger pranks.

Auto-Startup: Boots silently on logon via a hidden VBScript launcher.

Auto-Update: Periodically checks a remote URL for updates and self-updates without manual intervention.

Extensible Pranks: Easily add or modify prank functions in server.pyw.

Requirements

Windows 7 or newer

Python 3.7+ installed (added to PATH)

PyAutoGUI Python package

Installation

Run the installer: Execute setup_prank.bat, which will:

Create the %APPDATA%\PrankServer directory

Download the latest server.pyw

Add a firewall rule for TCP port 9999 (requires admin)

Deploy the launcher: Copy run_prank.vbs into your user’s Startup folder (shell:startup), alongside server.pyw.

Client Setup: Run client.py from your own machine, pointing at the target PC’s IP address.

Usage

On the target PC, ensure server.pyw is running (it auto-starts at logon).

From your PC, run:

python client.py <TARGET_IP>

Select from the command menu to trigger pranks.

Disclaimer & Legal

Consent Required: Only use this software on computers and networks for which you have explicit permission.

Harmless Pranks Only: Do not use to interfere with critical systems, disrupt business operations, or infringe on privacy.

No Warranty: This software is provided "as-is", without warranty of any kind, express or implied.

Limitation of Liability: Under no circumstances shall the author be liable for any direct, indirect, incidental, special, punitive, or consequential damages whatsoever arising out of or in connection with the use or inability to use this software.

Indemnification: You agree to indemnify, defend, and hold harmless the author from and against any claims, damages, losses, liabilities, and expenses arising out of your use of this software.

License

This project is released under the MIT License. See LICENSE for details.
