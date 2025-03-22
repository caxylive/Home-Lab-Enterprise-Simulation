<a name="top"></a>
[Back to Main](https://github.com/caxylive/Home-Lab-Enterprise-Simulation/tree/main)

---

# Installing Firefox via Snap

---

## 1. Update the System: Run the following command to ensure your system is up-to-date:
```Bash
sudo apt update
```

## 2. Install Snap (if not already installed): If Snap isn't installed, add it with:
```Bash
sudo apt install snapd
```

## 3. Install Firefox: Use Snap to install Firefox:
```Bash
sudo snap install firefox
```

## 4. Verify Installation: Ensure Firefox is installed by listing Snap applications:
```Bash
snap list
```
Firefox should appear in the output.

## 5. Launch Firefo: Run Firefox directly using:
```Bash
/snap/bin/firex
```

[Back to Top](#top)

---

# Creating a `.desktop` Shortcut for Firefox

---

## 1. Locate the Applications Directory: Most shortcuts are stored in ```/usr/share/applications```.

## 2. Create a `.desktop` File: Run the following command to create a desktop entry:
```Bash
sudo nano /usr/share/applications/firefox.desktop
```

## 3. Add the Shortcut Content: copy and paste the following into the file:
```Plaintext
[Desktop Entry]
Name=Firefox
Comment=Web Browser
Exec=/snap/bin/firefox
Icon=firefox
Terminal=false
Type=Application
Categories=Network;WebBrowser;
```

## 4. Save and Exit:
* Press `Ctrl + O` to save.
* Press `Ctrl + X` to exit.

## 5. Refresh the Menu: Your system should automatically detect the new shortcut. If not, log out and back in to update the application menu.

[Back to Top](#top)

---
