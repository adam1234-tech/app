# Building AdamApp for Windows (x86_64)

The Windows installer cannot be compiled on Linux or macOS. The project's own
CI builds it on a Windows runner, and that is the easiest route.

## Build on GitHub (no local setup)

1. Create the repository `https://github.com/adam1234-tech/app` and push this
   folder to it (`git init`, `git add -A`, `git commit`, `git push`).
2. Open the repository's **Actions** tab and enable workflows if asked.
3. Choose **Build Windows (AdamApp, x86_64 only)**, then **Run workflow**
   (leave `ref` empty to build `main`).
4. When the run finishes (expect 1 to 3 hours the first time), download the
   artifact **Concat-windows-x86_64**. It holds:
   - `Concat-0.2.12-windows-x86_64-setup.exe` - the installer (Inno Setup)
   - `Concat-0.2.12-windows-x86_64.msi` - the same for administrators
   The installer is branded AdamApp inside (title, Start menu, install folder,
   exe properties). Only the file name still says Concat; you may rename it.
5. The build is unsigned unless you add the repository secrets
   `WINDOWS_CERTIFICATE_PFX` and `WINDOWS_CERTIFICATE_PASSWORD`, so Windows
   SmartScreen will warn on first run ("More info" -> "Run anyway").

## Notes

- `.github/workflows/build-windows.yml` is `build-app.yml` cut down to the
  Windows x86_64 job. The original `build-app.yml` is unchanged.
- This is a modified version of Concat (AGPL-3.0-or-later). Keep `LICENSE`,
  `THIRD_PARTY_NOTICES.md` and the copyright headers, and make the source of
  any build you distribute available to its users.
- Settings > Version checks releases of `adam1234-tech/app`. Each release needs a
  `manifest.json` asset, as upstream's releases have.
