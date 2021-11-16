# How to get XRDP running on Manjaro GNOME

### Basic stuff:
- create/modify `/etc/X11/Xwrapper.config` with content `allowed_users=anybody`
- remove `--exit-with-session` from `~/.xinitrc`
- install `xorgxrdp` (not only `xrdp`)

### Fixing the "Oh no. Something has gone wrong." issue:
- Apply [this hack](https://github.com/matt335672/pam_close_systemd_system_dbus) from [matt335672](https://github.com/):
  - clone the repo with `git clone https://github.com/matt335672/pam_close_systemd_system_dbus`
  - run `sudo make install`
  - modify `/etc/pam.d/xrdp-sesman` as described in the repo's README
  - Explanation: [#1684](https://github.com/neutrinolabs/xrdp/issues/1684)
- Alternatively remove `pam_systemd_home.so` entries from /etc/pam.d/system-auth. Applying the hack is not necessary then.

### For NVIDIA this may be necessary:
_Add_ this to `/etc/xrdp/sesman.ini`:
```ini
[Xorg]
param=...
param=-layout # This line is new.
param=X11 Server # This line is new.
```
