# DuoM

This repository keeps the Android/Rust project source in `trinitymax_android.zip`.
GitHub Actions extracts that archive into the runner workspace and then attempts
to build the Android APK and standalone server binary.

## Repository layout

```text
DuoM/
├── .github/
│   └── workflows/
│       └── unzip-and-build.yml
├── README.md
└── trinitymax_android.zip
```

## Build with GitHub Actions

1. Upload the contents of this repository ZIP to the root of your GitHub repository.
2. Keep `trinitymax_android.zip` at the repository root.
3. Open **Actions** and enable workflows if GitHub asks.
4. Run **DuoM Android Build** manually, or push a change to the ZIP/workflow on `main` or `master`.
5. When the run completes, open its **Artifacts** section and download
   `DuoM-Android-APKs-and-server`.

The workflow extracts the ZIP, copies all files (including hidden files) into
the runner workspace, applies the known Bedrock MOTD format-string fix when
the source still matches the old line, builds Rust libraries for four Android
ABIs, builds the standalone server, and runs Gradle `assembleDebug`.

## Important project status

A successful build only means the included source compiled and packaged. The
source currently describes a Minecraft listener/handshake prototype; this
repository does not guarantee complete Java/Bedrock gameplay compatibility.
