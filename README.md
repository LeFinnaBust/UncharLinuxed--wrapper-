[README.md](https://github.com/user-attachments/files/33471648/README.md)
# Uncharted NDC – Linux AppImage

Unofficial AppImage wrapper for [SuperMedo's Uncharted: The Nathan Drake Collection PC port](https://github.com/Supermedo/uncharted_pc).
It is **not** a Linux port: the port is a Windows build, and this runs it through Proton.

- Nothing from the port is redistributed here. On first run the AppImage downloads the latest
  `uncharted-windows.zip` from the upstream release page and, if no Proton is found, the latest
  [GE-Proton](https://github.com/GloriousEggroll/proton-ge-custom) (checksum verified).
- **No game files.** You need your own decrypted PS4 dump (the folder with `eboot.bin`).
- Not affiliated with SuperMedo, Sony or Naughty Dog.

## Use
```bash
chmod +x Uncharted-NDC-x86_64.AppImage
./Uncharted-NDC-x86_64.AppImage          # launcher; pick your game folder (Linux files show up under Z:)
./Uncharted-NDC-x86_64.AppImage --play   # start straight away with saved launcher settings
```
Steam Deck: Desktop Mode → Steam → *Add a Non-Steam Game* → pick the AppImage. Leave Proton compatibility **off**
for that shortcut (the AppImage manages Proton itself).

## Updates
- On launch (at most every 6 h) it compares the installed port with the newest upstream release and asks before
  updating. Saves, shader caches and settings are kept. `--update` forces a check; `UNCHARTED_NO_UPDATE_CHECK=1` disables it.
- The port's own launcher also has an update button/check; both work on the same folder.
- `--update-runtime` fetches the newest GE-Proton. Release builds also embed AppImageUpdate info for the wrapper itself.

## Runner order
`umu-run` if installed → Proton found automatically (this app's own GE-Proton, GE-Proton or Proton 9+ from Steam) →
downloads GE-Proton → system `wine`. Override with `UNCHARTED_RUNNER=umu|proton|wine` or `UNCHARTED_PROTON=/path/to/proton`.

Needs `curl` and `python3` (present on SteamOS and most distros). Data lives in `~/.local/share/uncharted-appimage`
(`UNCHARTED_HOME` to change). Logs: `app/user/last_run.log`.

## Build / release
`./build.sh` builds the AppImage. Pushing a `v*` tag builds and publishes it via GitHub Actions.
