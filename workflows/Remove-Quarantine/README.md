# Remove Quarantine

A macOS Quick Action that strips the quarantine flag off files and folders, and re-signs broken app bundles so they'll actually open on Apple Silicon. Right-click, pick it from the menu, done.

## What it does

When you download something, macOS tags it with a quarantine attribute called `com.apple.quarantine`. That tag is what triggers the "are you sure you want to open this" warnings, and on Apple Silicon it's what causes the "app is damaged and can't be opened" error.

This Quick Action does two things to whatever you select:

1. Removes the quarantine attribute, recursively. If you point it at a folder, everything inside gets cleared too.
2. If the item is an app and its code signature is broken or missing, it ad-hoc re-signs it. Apple Silicon won't run unsigned code, so this is the part that turns a "damaged" app back into one that launches. It only re-signs apps that actually fail a signature check, so properly signed apps are left alone.

You get a notification when it's finished.

## Requirements

Any recent version of macOS. Works on both Apple Silicon and Intel. It only uses tools that ship with macOS (`xattr` and `codesign`), so there's nothing to install and nothing extra to download.

## Download

[Download Remove-Quarantine-QuickAction.zip](https://github.com/pacnpal/macos-workflows-scripts-shortcuts/raw/refs/heads/main/workflows/Remove-Quarantine/Remove-Quarantine-QuickAction.zip)

## Install

1. Download the zip and double-click it to unzip. You'll get a file named `Remove Quarantine.workflow`.
2. Double-click `Remove Quarantine.workflow`. macOS will ask if you want to install it. Click **Install**.
3. Done. It's now installed under your account in `~/Library/Services`.

Install it by double-clicking. Don't drag the file into a folder by hand. The double-click installer is the thing that registers it with the system. If you drag it in manually, the file gets copied but the menu item never shows up. This trips people up, so it's worth getting right the first time.

## If it doesn't show up in the menu

The Install step usually handles everything. If the menu item is missing, turn it on:

- **System Settings > General > Login Items & Extensions.** Scroll down to Extensions, click the Finder category, and check that **Remove Quarantine** is on.
- It can also appear under **System Settings > Keyboard > Keyboard Shortcuts > Services > Files and Folders.** Check it there too.

Quit System Settings all the way (Cmd+Q, not just closing the window) and reopen it if the toggle doesn't stick.

If it's still missing, there's one fix that always works. Open the workflow in Automator and save it:

1. Find `Remove Quarantine.workflow`. After install it lives in `~/Library/Services`.
2. Right-click it and choose Open With > Automator.
3. When it opens, press **Cmd+S**.

Saving from Automator re-registers it correctly. After that it shows up.

## How to use it

1. Select one or more files, folders, or apps in Finder. You can mix them in one selection.
2. Right-click and go to **Quick Actions > Remove Quarantine**. On some Macs it sits under the **Services** submenu instead.
3. Wait for the notification. The app or file will open normally now.

## Is it safe

It runs two standard macOS commands and nothing else. You can read the whole thing yourself: open it in Automator and look at the Run Shell Script step, or open the bundle and read `Contents/document.wflow`.

Removing quarantine and re-signing both turn off a security check, so the obvious rule applies. Only run this on things you actually trust. It's built for apps and files you downloaded on purpose from a source you know, not for getting past the warning on something sketchy.
