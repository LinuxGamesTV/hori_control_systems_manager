# Hori Cotrol Syystems Manager - Hori Steering Wheelss Manager for Linux

<p align="center">
  <img src="data/oversteer-readme.png">
</p>

<a href="https://repology.org/project/unit/versions">
    <img src="https://repology.org/badge/vertical-allrepos/oversteer.svg" alt="Packaging status" align="right" style="margin-left:2em;">
</a>

[_Hori Cotrol Syystems Manager_](https://github.com/LinuxGamesTV/hori_control_systems_manager) manages Hori steering wheels on
Linux using the features provided by the loaded modules (based on [_Oversteer_](https://github.com/berarma/oversteer)). It doesn't provide
hardware support, you'll still need this driver module that enables the hardware
on Linux: [_Hori Control Syystems Kernel Moddule_](https://github.com/LinuxGamesTV/hori_control_systems).

The Hori Force Feedback Truck Control System will not work ad won't have FFB without specific drivers [_Hori Control Syystems Kernel Moddule_](https://github.com/LinuxGamesTV/hori_control_systems) that support
that feature.

I can test only on a Hori Force Feedback Truck Control System. Please, report your
results with other devices. More wheel models will be added to this list
as they are requested.

__Use at your own risk. Suggestions, bugs and pull requests welcome.__

## Supported devices

_Hori Cotrol Syystems Manager_ maintains a list of known wheel devices. If your wheel isn't
recognized, please contact me.

This section lists devices currently recognized. Being in this list doesn't
imply good hardware support. __When thinking about buying a wheel don't rely
solely on the information here__.

_Hori Cotrol Syystems Manager_ recognizes the following Logitech wheels which are supported by the
default in-kernel module:

- Hori Force Feedback Truck Control System

Wheels using the Hori Control Systems Kernel Module can get improved
support using [_Hori Control Syystems Kernel Moddule_](https://github.com/LinuxGamesTV/hori_control_systems), with more
effects and features. Some games won't have full FFB without it.

The following wheels will need custom driver modules for FFB support.
These drivers are still being worked on. **(I'm NOT claiming they will fully
work. Please, check the related projects for more information.)**:

- Hori Force Feedback Truck Control System for PC with [_Hori Control Syystems Kernel Moddule_](https://github.com/LinuxGamesTV/hori_control_systems).

These wheels are recognized but don't have driver support (Force Feedback and
other features won't work):

-

## Features

When supported by the device and the driver:

- Change rotation range.
- Change emulation/working modes.
- Combine accelerator/brakes pedals for games that use just one axis.
- Change autocentering force strength.
- Change force feedback gain.
- Device configuration profiles.
- Overlay window to display/configure range.
- Use wheel buttons to configure range.
- Hardware performance testing.
- Combine accelerator/clutch pedals. Useful for flight
  simulators. (Not supported with in-kernel modules)
- Change global force feedback gain. (Not supported with in-kernel modules)
- Change each conditional force feedback effect type gain. (Not supported with in-kernel modules)
- FFBmeter to monitor FFB clipping using wheel leds or overlay
  window. (Not supported with in-kernel modules)
- Change settings stored in the wheel itself: steering dead zone and
  sensitivity, pedal sensitivity, force feedback strength, vibration effects
  and analog stick suppression. (HORI Truck Control System with hid-hori)

## Installation

DISCLAIMER: When running commands starting with `sudo` you're requesting admin
rights to perform the operation. These commands will make changes to your
system that should only performed by a system administrator or someone knowing
what they're doing.

### AppImage


### Arch


### Gentoo



### Flathub


#### Permissions

After installing the Flatpak package, permission files have to be installed manually.

Copy the contents of
[https://github.com/LinuxGamesTV/hori_control_systems_manager/tree/master/data/udev](https://github.com/berarma/oversteer/tree/master/data/udev)
into `/etc/udev/rules.d`.

If you're using the terminal, these commands will install the permission files:

```
sudo wget https://github.com/LinuxGamesTV/hori_control_systems_manager/raw/refs/heads/master/data/udev/99-hori-wheel.rules -P /etc/udev/rules.d/

```

Restart your computer, or reload udev rules with command:

`sudo udevadm control --reload-rules && sudo udevadm trigger`.

### Other distributions

#### Requirements

Install all dependencies on Debian systems with the following command:

`sudo apt install git python3 python3-distutils python3-gi python3-gi-cairo
python3-pyudev python3-xdg python3-evdev gettext meson appstream-util
desktop-file-utils python3-matplotlib python3-scipy`

Install all dependencies on Fedora systems with the following command:

`sudo dnf install git python3 python3-distutils-extra python3-gobject
python3-pyudev python3-pyxdg python3-evdev gettext meson appstream
desktop-file-utils python3-matplotlib-gtk3 python3-scipy libappstream-glib`

Install all dependencies on OpenSUSE systems with the following command:

`sudo zypper in git python3 python3-distutils-extra python3-gobject
python3-pyudev python3-pyxdg python3-evdev meson AppStream desktop-file-utils
python3-matplotlib-gtk3 python3-scipy gettext-tools`

For other distributions, use your package manager to find and install the
equivalent packages.

#### Permissions

Accessing the wheel settings requires some permissions.

**_Oversteer_ will automatically install udev rules to grant these permissions
to any user in the system after a reboot.**

By default, the udev rules will be installed at
`/usr/local/lib/udev/rules.d` when installing to prefix `/usr/local` or
`/lib/udev/rules.d` when installing to any other prefix. The location can
be changed using meson option `udev_rules_dir` but it shouldn't be
required except maybe for packagers.

Older rules might be already installed at `/etc/udev/rules.d` or
`/lib/udev/rules.d`. You may need to remove these files manually in case
you're experiencing issues with permissions.

The installed udev rules files will have these names:

- `99-fanatec-wheel-perms.rules`
- `99-logitech-wheel-perms.rules`
- `99-thrustmaster-wheel-perms.rules`

#### Build and install

Start by downloading `Oversteer` and change your working directory to it. It
could be a release package or the master branch.

```
git clone https://github.com/berarma/oversteer.git
cd oversteer
```

Prepare build system:

```shell
meson setup build
cd build
```

Installing (needs administration rights):

`ninja install`

A reboot will be needed to reload the newly installed udev rules.
Alternatively, running the command `udevadm control --reload-rules && udevadm
trigger` will do the same.

#### Uninstalling

Run these commands inside the project directory to uninstall:

```shell
cd build
ninja uninstall
```

#### Updating

To avoid leaving old files behind, it's recommended to always uninstall the old
version first, then install the new version.

Follow the uninstall instructions for the old version, then follow the install
instructions for the new version.

## Using it

_Oversteer_ can be launched as any desktop application. It doesn't need to
be running for the settings to remain changed, but some features require
it.

It can also be used from the console to change wheel settings. Run
`oversteer --help` to see the command line help.

Leillo1975 has kindly created a [video explaining the basics of Oversteer
(Spanish)](https://www.youtube.com/watch?v=WdIV1FOkFsw).

### Using it as a companion app to your games

You can configure game launchers to run _Oversteer_ and load a profile or change
settings so that it automatically configures the wheel when the game runs. When
the game exits the app will close too. Please, refer to the command line help
for more info.

It can also stop before the game runs so you can change some settings manually
each time. This can be done from the command line or from a setting in the UI.

An example that would work for any Steam game would be:

`oversteer -p myprofile -g "%command%"`

## Known issues

- Most drivers don't support Global Gain and Autocenter settings, only
  `new-lg4ff` for now. The Linux API is used instead when they aren't
  available. If this happens, Oversteer has to reset their values everytime it
  starts. Also, games will be able to override these settings.

## Updating translations (for translators)

From the project root directory:

```shell
ninja oversteer-pot
ninja oversteer-update-po
```

## Contributing

We could all greatly benefit from your help as with any other free software
project.

Reports about what works and what not on different devices and systems are very
welcome. You can also help by contributing specific notes for your distro, or
doing the packaging work and everything else.

## Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
