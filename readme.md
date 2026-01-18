# Mallorn: Watcher of the Heartwood

![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![AI](https://img.shields.io/badge/AI-Random_Forest-orange?style=for-the-badge)

**Mallorn** is a next-generation storage health monitoring tool. Unlike traditional tools that rely on manufacturer-defined "thresholds" (which often trigger too late), Mallorn uses a Random Forest Classifier trained on over 300,000 drive-days of data to detect non-linear patterns of imminent failure.

> "The standard 'Healthy' status is often a lie. Mallorn looks at the raw physics of the drive to tell you the truth."

## 🚀 Download & Install

**[Download for Windows (v1.0)](https://github.com/YOUR_USERNAME/Lightspire-Mallorn/releases/latest/download/Mallorn_Setup.exe)**

1.  **Download** the latest `Mallorn_Setup.exe` from the Releases section.
2.  **Run** the installer.
    *   *Note: If you see a "Windows protected your PC" popup, click **More Info** → **Run Anyway**.*
3.  **Launch** Mallorn.

---

## 🧠 The AI Core

Mallorn utilizes a supervised Machine Learning model trained on the Backblaze Data Center corpus (Q3 2023 snapshot).

### The Challenge
Hard drive failure data is extremely imbalanced (thousands of healthy days for every single failure). Standard models trained on this data simply guess "Healthy" every time to achieve 99.9% accuracy, missing the actual failures.

### Our Solution
We utilized undersampling techniques to create a balanced dataset, forcing the model to learn the subtle distinctions between a "used" drive and a "dying" drive.

* **Algorithm:** Random Forest Classifier (100 Estimators, Gini Impurity).
* **Input Features:** Raw values (not normalized) of the "Four Horsemen" of failure:
    * *SMART 5:* Reallocated Sectors
    * *SMART 187:* Reported Uncorrectable Errors
    * *SMART 197:* Current Pending Sectors
    * *SMART 9:* Power-On Hours
* **Validation:** ~93% accuracy on the validation set.

---

## ⚡ Key Features

### 1. Hybrid Scanning Engine
Mallorn employs a tiered discovery system to ensure no drive is left behind:
* **Tier 1 (Direct Metal):** Uses `smartctl` to access the physical controller. It cycles through NVMe, ATA, and CSMI protocols to bypass locked drivers (e.g., Intel RST).
* **Tier 2 (OS Fallback):** If direct access is blocked, Mallorn queries the Windows Storage Subsystem API via PowerShell to retrieve wear leveling and error counts kernel-side.
* **Tier 3 (Blocklist):** Intelligently filters out virtual drives and software loops.

### 2. Risk & Confidence Scoring
* **Risk Score:** A 0-100% probability metric indicating near-term failure likelihood.
* **Confidence Meter:** A "Consensus Score" derived from the internal voting of the 100 decision trees within the Random Forest.

### 3. Silent Monitoring
* **System Tray Integration:** Runs quietly in the background (`pystray`).
* **Daily Autoscan:** A background scheduler checks drive health every 24 hours.
* **Toast Notifications:** Uses native Windows notifications to alert you only when risks are detected.

### 4. Historical Analytics
* **SQLite Database:** All scan results are persisted locally.
* **Trend Analysis:** Interactive charts (`Chart.js`) allow you to visualize degradation trends over time.

### 5. Dynamic Theming
Switch themes instantly without restarting. Includes:
* **Mallorn:** (Default) Deep slate and bio-luminescent blue.
* **Isengard:** Industrial dark reds and oranges.
* **Mithril:** Clean silver and soft blues.
* **Lothlórien:** Forest greens and ancient gold.
* **Valinor:** High-contrast light mode (White & Gold).

## 🎨 Visual Customization
Mallorn features a dynamic theme engine. Users can switch styles instantly to match their OS or setup.

| **Mallorn (Default)** | **Valinor (Light Mode)** |
|:---:|:---:|
| ![Mallorn Theme](assets/theme-mallorn.png) | ![Valinor Theme](assets/theme-valinor.png) |

| **Isengard (Critical)** | **Lothlórien (Forest)** |
|:---:|:---:|
| ![Isengard Theme](assets/theme-isengard.png) | ![Lothlorien Theme](assets/theme-lothlorien.png) |

### Settings & Configuration
![Settings UI](assets/ui-settings.png)
---

## 🛠️ Technical Stack

| Component | Technology | Purpose |
| :--- | :--- | :--- |
| **Backend** | Python 3.12 | Core logic, resource management, threading. |
| **AI Model** | Scikit-Learn | Random Forest Classifier (`.pkl`). |
| **GUI** | PyWebView | Renders HTML/JS as a native desktop window. |
| **Hardware** | Smartmontools | `smartctl.exe` binary integration for raw access. |
| **Frontend** | HTML5 / CSS3 | Responsive UI with glassmorphism effects. |
| **Charts** | Chart.js | Historical data visualization. |
| **Database** | SQLite3 | Local storage of scan history and settings. |

---

## ⚖️ Third-Party Licenses

This application bundles **Smartmontools** (`smartctl`), which is free software licensed under the GNU General Public License (GPL).

* **Project Home:** [https://www.smartmontools.org](https://www.smartmontools.org)
* **License:** See `LICENSE-smartmontools.txt` included in this directory.
* **Source Code:** You can obtain the source code for Smartmontools from their website or by contacting us.

---

**Mallorn Sentinel © 2026. All Rights Reserved.**


