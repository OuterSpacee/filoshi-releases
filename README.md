# Filoshi Cross-Platform Binary Builder

This repository builds cross-platform binaries for the Filoshi desktop app.

## 📋 What This Builds

| Binary | Platform | Source |
|--------|----------|--------|
| `gs-x86_64-apple-darwin` | macOS Intel | Built from Ghostscript 10.04.0 source |
| `gs-aarch64-apple-darwin` | macOS ARM (Apple Silicon) | Built from Ghostscript 10.04.0 source |
| `gs-x86_64-unknown-linux-gnu` | Linux x86_64 | Built from Ghostscript 10.04.0 source |
| `magick-x86_64-unknown-linux-gnu` | Linux x86_64 | Built from ImageMagick 7.1.2-15 source |

## 🚀 How to Use

### Option 1: Manual Trigger (Recommended)
1. Push this repository to GitHub
2. Go to **Actions** tab
3. Select **"Build Cross-Platform Binaries"**
4. Click **"Run workflow"**
5. Wait ~15-20 minutes for builds to complete
6. Download binaries from the created release

### Option 2: Tag Push
Push a tag like `binaries-v1.0.0` to trigger automatic build:
```bash
git tag binaries-v1.0.0
git push origin binaries-v1.0.0
```

## 📦 After Build

Binaries will be available in GitHub Releases:
- Go to your repo's **Releases** page
- Download the release assets
- Extract and place in `filoshi/apps/desktop/src-tauri/binaries/`
- **Remove file extensions** (Linux/macOS binaries don't use `.exe`)

## ⚙️ Build Details

### macOS Builds
- **Intel**: Runs on `macos-13` (x86_64)
- **ARM**: Runs on `macos-14` (M1/M2 Apple Silicon)
- **Dependencies**: Installed via Homebrew
- **Build**: Static linking with `--disable-shared --enable-static`

### Linux Build
- **Runner**: `ubuntu-22.04` (x86_64)
- **Dependencies**: Installed via apt
- **Build**: Static linking for portability

## 🔧 Customization

To change versions, edit these lines in `.github/workflows/build-binaries.yml`:
```yaml
env:
  GHOSTSCRIPT_VERSION: "10.04.0"      # Change Ghostscript version
  IMAGEMAGICK_VERSION: "7.1.2-15"      # Change ImageMagick version
```

## ⏱️ Build Times

| Job | Estimated Time |
|-----|----------------|
| macOS Intel | ~8-10 minutes |
| macOS ARM | ~8-10 minutes |
| Linux | ~10-15 minutes |
| **Total** | **~15-20 minutes** |

## 📝 Notes

- Binaries are statically linked for portability
- No external dependencies required on target systems
- Built with minimal features (no X11, no CUPS, etc.) for smaller size
- GitHub Actions runners are free for public repositories
