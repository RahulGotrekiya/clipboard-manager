# 📋 Clipboard Manager Documentation

A Wayland and X11 compatible clipboard history manager with rofi integration, auto-paste functionality, and a centered display.

## 🔍 Overview

This clipboard manager script enhances your desktop experience by maintaining a history of clipboard items, allowing you to:

- View and recall previously copied items
- Automatically paste selected items to the active window
- Delete specific clipboard history entries
- Clear the entire clipboard history

The script uses `cliphist` for clipboard history management, `rofi` for the UI, and `wl-clipboard` for clipboard operations.

## 📦 Dependencies

- **Required**:
  - `cliphist`: Clipboard history management
  - `wl-clipboard`: Wayland clipboard utilities
  - `rofi`: Application launcher and general menu
- **Optional**:
  - `wtype` (Wayland) or `xdotool` (X11): For auto-paste functionality
  - `notify-send`: For desktop notifications
  - `jq`: For parsing window information in Hyprland

## 💾 Installation

1. Save the script to a location of your choice (e.g., `~/.local/bin/clipboard-manager.sh`)
2. Make it executable:

   ```bash
   chmod +x ~/.local/bin/clipboard-manager.sh
   ```

3. Ensure all dependencies are installed according to your distribution

## ⚙️ Configuration

The script automatically looks for a rofi configuration file at:

```
~/.config/rofi/clipboard.rasi
```

### Configuration Variables

You can customize appearance by setting these environment variables:

- `ROFI_SCALE`: Font size for the rofi menu (default: 10)
- `HYPR_BORDER`: Border width based on your Hyprland settings (default: 1)

## 🚀 Usage

### Basic Commands

```bash
# Display clipboard history, copy selected item and paste it
clipboard-manager.sh -c  # or --copy or just c

# Display clipboard history and delete selected item
clipboard-manager.sh -d  # or --delete

# Clear the entire clipboard history database
clipboard-manager.sh -w  # or --wipe
```

### ⌨️ Keyboard Shortcuts

For convenient usage, bind the script to keyboard shortcuts in your window manager or desktop environment:

#### Example for Hyprland:

Add to your `~/.config/hypr/hyprland.conf`:

```conf
# Clipboard manager
bind = SUPER, V, exec, ~/.local/bin/clipboard-manager.sh -c
bind = SUPER SHIFT, V, exec, ~/.local/bin/clipboard-manager.sh -d
bind = SUPER ALT, V, exec, ~/.local/bin/clipboard-manager.sh -w
```

## ✨ Features

### Centered Display

The script forces rofi to display centered on screen for better visibility.

### Auto-Paste Functionality

When using the copy action (`-c`), the script automatically:

1. Displays clipboard history
2. Copies the selected item to the clipboard
3. Simulates a paste action in the active window

### Environmental Detection

The script automatically detects:

- Wayland vs. X11 environment
- Presence of notification utilities
- Active window managers

### Empty Clipboard Handling

Shows appropriate notifications when the clipboard history is empty.

## 🔧 Troubleshooting

### Auto-Paste Not Working

- Ensure either `wtype` (Wayland) or `xdotool` (X11) is installed
- Some applications with custom clipboard handling may not support simulated paste commands

### Missing Clipboard Items

- Make sure the `cliphist` daemon is running
- Try restarting the clipboard daemon: `pkill cliphist; cliphist & disown`

### UI Display Issues

- Check your rofi configuration
- Verify the script can find your rofi configuration at `~/.config/rofi/clipboard.rasi`

## 🧩 Advanced Usage

### Integration with Other Scripts

You can call this script from other scripts or applications using the standard command-line arguments.

### Custom Styling

Create a custom rofi theme file at `~/.config/rofi/clipboard.rasi` to change the appearance of the clipboard manager menu.

---

Feel free to modify and distribute according to your needs 😊
