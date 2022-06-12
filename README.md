# cariboublocker for GNOME Shell 3.36 (and above)

Available at: https://extensions.gnome.org/extension/3222/block-caribou-36/

Based on https://github.com/keringar/cariboublocker.

Change some naming to be compatible with GNOME Shell 3.36.

There are some naming changes in GNOME Shell, so the original project by keringar no longer works on some GNOME Shell versions (For me, it works on Fedora 31 with gnome-shell-3.34.5 and Xorg, but not on Fedora 32 with gnome-shell-3.36.3 and Xorg).

## Install

### Way 1: use extensions.gnome.org
This extension is available at the official GNOME Shell Extensions website:
<https://extensions.gnome.org/extension/3222/block-caribou-36/>

### Way 2: download zip
Go to [Releases](https://github.com/lxylxy123456/cariboublocker/releases), and
choose the zip file corresponding to your gnome-shell version. Then
`gnome-extensions install <your-gnome-shell-version>.zip`.

## Installing on high GNOME Shell version

This extension is likely to work for a high GNOME Shell version, if GNOME
Shell's `keyboard.js` is not changed. This extension specifies a number of
supported GNOME Shell versions in `metadata.json`. If your GNOME Shell version
is not in this list, you may not be able to install this extension.

There are a few possible solutions:
1. In dconf, set `disable-extension-version-validation` (in
   `/org/gnome/shell/`) to True. See
   <https://gjs.guide/extensions/overview/anatomy.html#shell-version>.
2. Download this extension as a zip file, from either extensions.gnome.org or
   GitHub. Then add your GNOME Shell version number to `metadata.json` in
   the list specified by `"shell-version"`.
3. Wait for the extension maintainer (currently lxylxy123456) to update the
   extension. Maybe notifying the maintainer on extensions.gnome.org or GitHub
   can help.

## Test Log
* 13 Jun 2020: [3.36.3](3.36.3/) **PASS** on
  Fedora 32 with gnome-shell-3.36.3 and Xorg
* 20 Feb 2021: [3.36.3](3.36.3/) **PASS** on
  Fedora 33 with gnome-shell-3.38.4 and Xorg
* 29 Apr 2021: [40.0](40.0/) **PASS** on
  Fedora 34 with gnome-shell-40.0 and Xorg
* 5 Dec 2021: [41](41/) **PASS** on
  Fedora 35 with gnome-shell-41.1 and Xorg
* 12 Jun 2022: [42](42/) **PASS** on
  Fedora 36 with gnome-shell-42.2 and Xorg

## Change Log

### [3.36.3](3.36.3/)
* Replace `Keyboard` with `KeyboardManager` in `extensions.js`.

### [40.0](40.0/)
* Simply change `"shell-version"` in `metadata.json` to `40.0`. For some reason
  the version string `"3.36.3"` still works on Fedora 33's gnome-shell-3.38.

### [40](40/)
* Update `shell-version` in `metadata.json`

### [41](41/)
* Update `shell-version` in `metadata.json`

### [42](42/)
* Update `shell-version` and description to be more comprehensive

## Relevant Code

See `js/ui/keyboard.js`. Here are links for some versions after 3.36:

* <https://gitlab.gnome.org/GNOME/gnome-shell/-/blob/main/js/ui/keyboard.js>
* <https://gitlab.gnome.org/GNOME/gnome-shell/-/blob/gnome-42/js/ui/keyboard.js#L1174>
  <!-- 8dc0ca5eebdeda668418f02cd544b19589872fc6 -->
* <https://gitlab.gnome.org/GNOME/gnome-shell/-/blob/gnome-41/js/ui/keyboard.js#L1164>
  <!-- 040a5d34d7a5601ad2a2f622fd9a393c5e08be5f -->
* <https://gitlab.gnome.org/GNOME/gnome-shell/-/blob/gnome-40/js/ui/keyboard.js#L1167>
  <!-- 821ff3bb887cfbbc080dc737b6084282213d0e7b -->
* <https://gitlab.gnome.org/GNOME/gnome-shell/-/blob/gnome-3-38/js/ui/keyboard.js#L1129>
  <!-- cf9d73ed5d316093ad7284ce5df95bce51409f28 -->
* <https://gitlab.gnome.org/GNOME/gnome-shell/-/blob/gnome-3-36/js/ui/keyboard.js#L1130>
  <!-- 40a003e5acaddb74ddd3f02294b0b4bc01ac1d3f -->

The structure of code is:
```js
var KeyboardManager = class KeyBoardManager {
    constructor() {
        ...
    }

    _lastDeviceIsTouchscreen() {

        if (!this._lastDevice)
            return false;

        let deviceType = this._lastDevice.get_device_type();
        return deviceType == Clutter.InputDeviceType.TOUCHSCREEN_DEVICE;
    }

    ...
}
```

This extension simply replaces `_lastDeviceIsTouchscreen` with a function that
always returns false.

In GNOME Shell 3.34 and earlier, the class was named `Keyboard` instead of
`KeyboardManager`. So keringar's extension no longer works after GNOME Shell
3.36.

* <https://gitlab.gnome.org/GNOME/gnome-shell/-/blob/gnome-3-34/js/ui/keyboard.js#L1052>
  <!-- 3d7ee7856f1c3231925cce770d1fe0b3b3bb932d -->

## Development Hints

[Looking Glass](https://wiki.gnome.org/Projects/GnomeShell/LookingGlass) is very helpful for debugging (saves my time installing an IDE etc).

To create a zip file for https://extensions.gnome.org/upload/, use `zip -j a.zip extension.js metadata.json`

# Original README.md from https://github.com/keringar/cariboublocker

RESOLVED https://bugs.launchpad.net/ubuntu/+source/gnome-shell/+bug/1723857

## cariboublocker
Prevents caribou from appearing when you use a touchscreen with the on screen keyboard disabled

## Installation
1. https://extensions.gnome.org/extension/1326/block-caribou/
2. You may need to install an extension, Gnome Shell Integration, see the gnome extensions [about](https://extensions.gnome.org) page for more details.
3. Click the toggle flag in the top right to ON.
