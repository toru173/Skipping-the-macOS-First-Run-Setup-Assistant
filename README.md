# Skipping the macOS First Run Setup Assistant
 Mechanism to skip the macOS first-run setup assistant. Using this technique it is possible to skip the macOS first-run setup assistant known as macbuddy. This will allow the user to create a new local account with all standards/defaults, and not be prompted to sign in to iCloud etc.

This also has the added benefit of side-stepping DEP enrollment, though will not allow iCloud or firmware locked device from being used

## Steps
 1. Create a user installer package using Greg Neagle's fantastic [pycreateuserpkg](https://github.com/gregneagle/pycreateuserpkg). Set user details as desired. A pre-existing 'apple' user with password 'apple' is included in this repository as an example.
 2. Install macOS as normal, be it from a [bootable USB](https://support.apple.com/en-us/HT201372) or with [Recovery](https://support.apple.com/en-au/HT204904)
 3. Once install completed, restart the device and re-enter recovery mode. Ensure the user installer package from step 1 is available (perhaps on an external USB)
 4. Install the user with `installer -pkg /path/to/user/installer.pkg -target /Volumes/Newly\ Installed\ OS\ \- \Data/` (or the equivalent in non-ROSV targets)
 5. Once the install is complete, run the following (again, substitute for non-ROSV where appropriate):
   * `touch /Volumes/Newly\ Installed\ OS\ \- \Data/private/var/db/.AppleSetupDone`
   * `touch /Volumes/Newly\ Installed\ OS\ \- \Data/Library/User\ Template/English.lproj/.skipbuddy`
   * `touch /Volumes/Newly\ Installed\ OS\ \- \Data/Library/User\ Template/Additional\ Localizations\ As\ Appropriate/.skipbuddy`
6. Reboot the device. Allow to boot normally. If you have enabled auto-login, you will land at the desktop. If not simply enter the password configured in step 1 and enjoy the new install with all default settings

Example user package created with `./createuserpkg -n apple -u 501 -V 1.0 -i local.toru173.createappleuser -p apple -f Apple -a -A Create\ Apple\ User.pkg`

