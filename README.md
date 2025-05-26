# Muffin Tiling Gaps Patch

A native tiling gaps implementation for the Muffin window manager, providing seamless and configurable gaps between tiled windows in the Cinnamon desktop environment.

## 🎯 Overview

**Muffin** is the window manager for the Cinnamon desktop environment (used by Linux Mint and other distributions). This patch extends Muffin with **native tiling gaps support**, allowing you to add customizable spaces between windows when using window tiling features.

Unlike extension-based solutions that can cause visual glitches or race conditions, this patch integrates gaps directly into the window manager for reliable, seamless operation.

## ✨ Features

### Core Functionality

- **Native Integration**: Gaps are handled directly by Muffin, not through workarounds
- **Configurable Gap Sizes**: Separate settings for inner gaps (between windows) and outer gaps (screen edges)
- **Real-time Configuration**: Changes apply immediately without restart
- **System-wide Support**: Works with all tiling operations (keyboard shortcuts, mouse dragging, etc.)
- **No Visual Glitches**: Smooth, flicker-free gap rendering

### Configuration Options

- **Inner Gaps**: Spaces between adjacent tiled windows (0-100 pixels)
- **Outer Gaps**: Spaces between windows and screen edges (0-100 pixels)
- **Enable/Disable Toggle**: Easily turn gaps on/off without losing settings
- **Persistent Settings**: Configuration survives system restarts and updates

### Supported Tiling Operations

- Edge tiling (drag to screen edges)
- Keyboard shortcuts for window positioning
- Maximize/restore operations
- Quarter tiling (corner snapping)
- All existing Muffin tiling features

## 📋 Requirements

### System Requirements

- Linux system running Cinnamon desktop environment
- Linux Mint, Ubuntu Cinnamon, or other Cinnamon-based distributions
- Administrative privileges (sudo access)
- Basic terminal usage knowledge

### Build Dependencies

#### Ubuntu/Debian

```bash
sudo apt update
sudo apt install build-essential meson ninja-build gettext libglib2.0-dev \
  libmuffin-dev libgtk-3-dev libgirepository1.0-dev libjson-glib-dev \
  libx11-dev libxcomposite-dev libxdamage-dev libxext-dev libxfixes-dev \
  libxi-dev libxinerama-dev libxrandr-dev libxrender-dev libxres-dev \
  libxtst-dev libstartup-notification0-dev libsm-dev libice-dev \
  libcanberra-gtk3-dev libdbus-1-dev libsystemd-dev libgudev-1.0-dev \
  libinput-dev libudev-dev libxkbcommon-dev libxkbfile-dev \
  libxkbregistry-dev libxkbcommon-x11-dev libwayland-dev \
  libwayland-egl-backend-dev libegl1-mesa-dev libgles2-mesa-dev \
  libgbm-dev libdrm-dev libpam0g-dev libseccomp-dev libcap-dev
```

#### Arch Linux

```bash
sudo pacman -S base-devel meson ninja muffin gtk3 gobject-introspection \
  json-glib libx11 libxcomposite libxdamage libxext libxfixes libxi \
  libxinerama libxrandr libxrender libxres libxtst startup-notification \
  libsm libice libcanberra-gtk3 dbus systemd libgudev libinput libudev \
  xkbcommon xkbfile xkbregistry xkbcommon-x11 wayland wayland-egl mesa \
  gbm libdrm pam libseccomp libcap
```

#### Fedora

```bash
sudo dnf install @development-tools meson ninja-build muffin-devel \
  gtk3-devel gobject-introspection-devel json-glib-devel libX11-devel \
  libXcomposite-devel libXdamage-devel libXext-devel libXfixes-devel \
  libXi-devel libXinerama-devel libXrandr-devel libXrender-devel \
  libXres-devel libXtst-devel startup-notification-devel libSM-devel \
  libICE-devel libcanberra-gtk3-devel dbus-devel systemd-devel \
  libgudev1-devel libinput-devel libudev-devel libxkbcommon-devel \
  libxkbfile-devel libxkbregistry-devel libxkbcommon-x11-devel \
  wayland-devel wayland-egl-devel mesa-libEGL-devel mesa-libGLES-devel \
  mesa-libgbm-devel libdrm-devel pam-devel libseccomp-devel libcap-devel
```

## 🚀 Installation

### Quick Install

1. **Clone or download** this repository to your local machine
2. **Navigate** to the project directory:

   ```bash
   cd /path/to/muffin-tiling-gaps
   ```

3. **Run the installer**:

   ```bash
   ./install.sh
   ```

The installer will:

- Check dependencies and system compatibility
- Create a backup of your current Muffin installation
- Build the patched Muffin with tiling gaps support
- Install the new library and GSettings schemas
- Set up configuration tools
- Restart Cinnamon to load the new window manager

### Manual Installation Steps

If you prefer manual installation or need to troubleshoot:

1. **Install dependencies** (see Requirements section above)
2. **Configure the build**:

   ```bash
   meson build --prefix=/usr/local
   ```

3. **Compile**:

   ```bash
   ninja -C build
   ```

4. **Install**:

   ```bash
   sudo ninja -C build install
   sudo cp build/src/libmuffin.so.0.0.0 /usr/lib/libmuffin.so.0.0.0
   ```

5. **Compile schemas**:

   ```bash
   sudo glib-compile-schemas /usr/share/glib-2.0/schemas/
   ```

6. **Restart Cinnamon**:

   ```bash
   cinnamon --replace &
   ```

## ⚙️ Configuration

### GUI Configuration Tool

Launch the graphical configuration interface:

```bash
python3 tools/tiling-gaps-config.py
```

The GUI provides:

- Enable/disable toggle for tiling gaps
- Sliders for inner and outer gap sizes (0-100 pixels)
- Real-time preview of settings
- Reset to defaults button

### Command Line Interface

Use the `muffin-gaps` command for terminal-based configuration:

```bash
# Enable tiling gaps
./tools/muffin-gaps enable

# Disable tiling gaps
./tools/muffin-gaps disable

# Set inner gap size (between windows)
./tools/muffin-gaps set-inner 15

# Set outer gap size (screen edges)
./tools/muffin-gaps set-outer 10

# Check current status
./tools/muffin-gaps status

# Reset all settings to defaults
./tools/muffin-gaps reset

# Launch GUI configuration tool
./tools/muffin-gaps gui

# Show help
./tools/muffin-gaps help
```

### Direct GSettings Configuration

Advanced users can configure settings directly:

```bash
# Enable/disable gaps
gsettings set org.cinnamon.muffin tiling-gaps-enabled true

# Set gap sizes (0-100 pixels)
gsettings set org.cinnamon.muffin tiling-gap-size 15
gsettings set org.cinnamon.muffin tiling-outer-gap-size 10

# Check current values
gsettings get org.cinnamon.muffin tiling-gaps-enabled
gsettings get org.cinnamon.muffin tiling-gap-size
gsettings get org.cinnamon.muffin tiling-outer-gap-size
```

## 🎮 Usage

### Basic Usage

1. **Enable gaps** using any configuration method above
2. **Set your preferred gap sizes** (recommended: inner 10-20px, outer 5-15px)
3. **Use normal tiling operations**:
   - Drag windows to screen edges to tile them
   - Use keyboard shortcuts for window positioning
   - Double-click title bars to maximize windows
   - All operations will now include the configured gaps

### Testing the Installation

Run the verification script to ensure everything is working:

```bash
python3 tools/test-tiling-gaps.py
```

### Example Workflow

```bash
# Enable gaps and set sizes
./tools/muffin-gaps enable
./tools/muffin-gaps set-inner 15
./tools/muffin-gaps set-outer 10

# Test by dragging a window to the left edge of the screen
# The window should tile with gaps around it

# Check status
./tools/muffin-gaps status
```

## 🗑️ Uninstallation

To remove the tiling gaps patch and restore the original Muffin:

```bash
./uninstall.sh
```

The uninstaller will:

- Restore the original Muffin library from backup
- Reset GSettings to defaults
- Remove configuration tools
- Clean build artifacts
- Restart Cinnamon with the original window manager

### Manual Uninstallation

If the script fails, manually restore:

```bash
# Restore original library (if backup exists)
sudo cp ~/.muffin-gaps-backup/libmuffin.so.0.0.0.system /usr/lib/libmuffin.so.0.0.0

# Reset settings
gsettings reset org.cinnamon.muffin tiling-gaps-enabled
gsettings reset org.cinnamon.muffin tiling-gap-size
gsettings reset org.cinnamon.muffin tiling-outer-gap-size

# Restart Cinnamon
cinnamon --replace &
```

## 🔧 Troubleshooting

### Common Issues

**Installation fails with dependency errors**

- Ensure all build dependencies are installed for your distribution
- Update your package manager: `sudo apt update` (Ubuntu/Debian)

**Cinnamon crashes after installation**

- Run the uninstaller to restore the original Muffin
- Check system logs: `journalctl -xe`

**Gaps not appearing**

- Verify gaps are enabled: `./tools/muffin-gaps status`
- Try restarting Cinnamon: `cinnamon --replace &`
- Check if the patched library is loaded: `ldd /usr/bin/cinnamon`

**Settings not persisting**

- Ensure GSettings schemas are compiled: `sudo glib-compile-schemas /usr/share/glib-2.0/schemas/`
- Check schema installation: `gsettings list-schemas | grep muffin`

**System updates overwrite the patch**

- Re-run the installer after system updates that affect Muffin
- The installer preserves your settings and backup

### Getting Help

1. **Check the logs** generated by install/uninstall scripts
2. **Verify installation** with the test script: `python3 tools/test-tiling-gaps.py`
3. **Review system logs** for Cinnamon/Muffin errors
4. **Try safe mode**: Boot with original Muffin using the uninstaller

## 🔬 Technical Details

### How It Works

This patch modifies Muffin's window management code to:

- Add gap calculations to tiling operations
- Integrate with GSettings for configuration
- Preserve existing tiling behavior while adding gap support
- Handle edge cases like maximized windows and multi-monitor setups

### Files Modified

- **Window management**: Core tiling logic enhanced with gap calculations
- **GSettings schema**: New configuration keys for gap settings
- **Build system**: Meson configuration updated for new components

### Architecture

- **Native implementation**: Gaps are calculated at the window manager level
- **GSettings integration**: Real-time configuration without restart
- **Backward compatibility**: All existing Muffin features remain unchanged

## 🤝 Contributing

Contributions are welcome! This project enhances the Cinnamon desktop experience.

### Development Setup

1. Fork the repository
2. Install development dependencies
3. Make your changes
4. Test thoroughly with the provided tools
5. Submit a pull request

### Reporting Issues

- Use the test script to verify your installation
- Include system information (distribution, Cinnamon version)
- Provide relevant log output from install/uninstall scripts

## 📄 License

This project is licensed under the GNU General Public License v2.0 or later, consistent with the original Muffin project.

## 🙏 Acknowledgments

- **Muffin/Mutter developers** for the excellent window manager foundation
- **Cinnamon team** for the desktop environment
- **Linux Mint** for maintaining and improving the Cinnamon experience

---

**Note**: This patch is designed specifically for Muffin/Cinnamon. For other window managers, consider alternatives like i3-gaps, bspwm, or similar tiling window managers with built-in gap support.
