# Microsoft Office 2016 KMS Activation Batch Script

> **For educational, research, and analysis purposes only.**  
> This repository provides a Windows Batch script that demonstrates the internal workflow of KMS-based activation for Microsoft Office 2016. It is **not** intended to bypass Microsoft’s licensing terms or to activate unlicensed copies of Office.

---

## 📖 Overview

This script automates the process of configuring and attempting KMS activation for **Microsoft Office 2016 Volume License** editions. It uses native Windows tools (the Office Software Protection Platform script – `ospp.vbs`) and does not rely on third‑party binaries.

By studying this script, you can learn:
- How Office volume license installations are detected.
- How product keys (GVLK) and KMS host settings are applied.
- How activation status is queried and reported.

---

## ✨ Features

- ✔️ Detects existing Office 2016 Volume License installations (Standard / Professional Plus).
- ✔️ Installs the required volume license files (if missing).
- ✔️ Sets the **Generic Volume License Key** (GVLK) for the detected edition.
- ✔️ Configures a KMS host address (user‑definable via a variable).
- ✔️ Attempts activation using the built‑in `ospp.vbs` script.
- ✔️ Displays detailed activation status and error codes.
- ✔️ Fully self‑contained – uses only Windows system components.
- ✔️ Silent operation (no pop‑ups) with console output for tracking.

---

## 📂 Supported Office Editions

| Product                     | Edition                     |
|-----------------------------|-----------------------------|
| Microsoft Office Standard 2016 | Volume License           |
| Microsoft Office Professional Plus 2016 | Volume License      |

> **Note:** This script **does not** work with retail (click‑to‑run) or OEM versions of Office. Only volume‑licensed media is supported.

---

## 🖥️ System Requirements

- **Operating System:** Windows 10 / Windows 11 (64‑bit or 32‑bit).
- **Microsoft Office:** Office 2016 Volume License edition already installed.
- **Privileges:** Administrator rights are required to modify Office licensing settings.
- **Network:** An internet connection is needed if your KMS server is remote (on‑premise KMS hosts are also supported).

---

## 🚀 How to Use This Script

Follow the steps below to run the activation script safely and effectively.

### 1. Download & Install Microsoft Office 2016 (Volume License)

- Obtain the official Volume License ISO or installation media from your authorized Microsoft reseller or your organization’s volume licensing portal.
- Run the installer and complete the installation.
- **Do not** enter a product key during installation – the script will apply the correct GVLK later.

### 2. Prepare Your System

- **Windows Defender / Antivirus:** Some security software may flag KMS activation scripts as potentially unwanted. This is a false positive due to the nature of the script (it modifies licensing settings).  
  Instead of disabling protection entirely, **add an exclusion** for the folder containing the batch file:
  - Open Windows Security → Virus & threat protection → Manage settings → Add or remove exclusions.
  - Exclude the folder where you placed the script.
- **Temporarily disable real‑time protection** only if you understand the risks, and re‑enable it immediately after the script completes.

### 3. Download the Activator Batch File

- Clone or download this repository to your local machine.
- Ensure the file is saved in a folder you have write permissions to (e.g., `C:\OfficeActivation`).

### 4. Run the Batch File as Administrator

- Right‑click the `activate_office2016.bat` file.
- Select **“Run as administrator”** from the context menu.
- A command prompt window will open and the script will begin executing.
- Follow any on‑screen prompts (if any) – the script is mostly automated.

### 5. Verify Activation

- After the script finishes, it will display the current activation status.
- You can also manually check by opening any Office application (e.g., Word) and going to **File → Account** – the product information should show “Product Activated” if successful.

---

## 🛠️ How the Script Works (Technical Breakdown)

This section explains each major step performed by the batch file.

| Step | Command / Action | Purpose |
|------|------------------|---------|
| **Detection** | `if exist "C:\Program Files\Microsoft Office\Office16\ospp.vbs" ...` | Locate the Office installation path. |
| **Licensing** | `cscript ospp.vbs /inslic:..."` | Install the volume license (.xrm-ms) files if missing. |
| **Key Setting** | `cscript ospp.vbs /setprt:"..."` | Set the Generic Volume License Key (GVLK) for the detected Office edition. |
| **Host Configuration** | `cscript ospp.vbs /sethst:"kms.example.com"` | Point to a KMS host (default value can be changed in the script). |
| **Activation Attempt** | `cscript ospp.vbs /act` | Request activation from the configured KMS server. |
| **Status Query** | `cscript ospp.vbs /dstatus` | Display current activation state and remaining grace period. |
| **Error Handling** | Checks `%errorlevel%` after each command and reports success/failure. | Provides clear feedback for troubleshooting. |

---

## 🔧 Configuration Options

You can customise the script by editing the following variables inside the `.bat` file:

| Variable        | Description                               | Example |
|-----------------|-------------------------------------------|---------|
| `KMS_HOST`      | The KMS server address or DNS name.       | `set KMS_HOST=kms.example.com` |
| `OFFICE_PATH`   | Override the default Office installation path. | `set OFFICE_PATH=C:\Program Files\Microsoft Office\Office16` |

> **Important:** A valid KMS server that is reachable from your network is required for activation to succeed. The script does not include any KMS server details by default – you must supply your own or use your organization's internal KMS.

---

## ❗ Troubleshooting

| Issue | Possible Solution |
|-------|-------------------|
| *“No Office installation found”* | Ensure Office 2016 is installed and is a volume‑licensed edition. |
| *“Access denied”* | Run the script as Administrator. |
| *“Error 0x80070005”* | Check that Windows Defender or other security software is not blocking the script. |
| *“Activation failed (0x8007232B)”* | The KMS host name could not be resolved. Verify `KMS_HOST` is correct and reachable. |
| *“Licensing files missing”* | The script will attempt to install them, but you may need to locate the correct `.xrm-ms` files from your Office installation media. |
| Script closes immediately | Open a Command Prompt as Administrator and run the batch file from there to see error messages. |

---

## ⚠️ Important Disclaimers

- **This script is provided strictly for educational and research purposes.** It is intended to help IT professionals, students, and enthusiasts understand the mechanisms of volume activation.
- **The script does not bypass product activation** – it merely configures the system to use KMS, which is a legitimate activation method for volume‑licensed products. Successful activation requires a valid KMS server and a genuine volume‑license agreement with Microsoft.
- **The author does not endorse or support unauthorized use** of Microsoft software. Users are solely responsible for ensuring that their use of this script complies with all applicable laws and Microsoft’s licensing terms.
- **Use at your own risk.** The script modifies system licensing components; while it is designed to be safe, you should always back up your system before running such scripts.

---

## 📜 License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing

Contributions that improve the educational value, fix bugs, or clarify documentation are welcome. Please submit a pull request or open an issue for discussion.

---

## 📧 Contact

For questions or suggestions, feel free to open an issue on GitHub.  
*Please do not ask for activation keys or KMS server addresses – this repository does not provide them.*

---

**Thank you for using this script responsibly.**  
Happy learning!
