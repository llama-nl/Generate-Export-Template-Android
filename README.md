# ðŸ¤– CI/CD: Android Export Template Builder

This repository includes a **GitHub Actions** workflow designed to
compile **custom Godot 4.x Android Export Templates** from source.

It is especially useful if you: - Need custom engine patches or
modules - Want **AES-256 GDScript encryption** - Want reproducible
Android export templates for CI/CD

------------------------------------------------------------------------

## âœ¨ Features

-   ðŸ”„ **Automatic Source Fetching** -- Clones the latest stable Godot
    release automatically
-   ðŸ“± **Multiâ€‘Architecture Support** -- Builds for **arm32 (v7)** and
    **arm64 (v8)**
-   ðŸŽ® **Swappy Integration** -- Android Frame Pacing for smoother
    rendering
-   ðŸ” **Security** -- Optional **AESâ€‘256 script encryption**
-   ðŸ“¦ **Artifacts Output**
    -   Android export template APKs
    -   `android_source.zip` for custom Gradle builds

------------------------------------------------------------------------

## ðŸ›  Prerequisites

### Required Repository Secret

This workflow **will fail early** if the encryption key is missing.

1.  Go to:

    **Settings â†’ Secrets and variables â†’ Actions â†’ New repository
    secret**

2.  Create the following secret:

```{=html}
<!-- -->
```
    Name:  SCRIPT_AES256_ENCRYPTION_KEY
    Value: <64â€‘character hexadecimal key>

Generate a key using OpenSSL:

``` bash
openssl rand -hex 32
```

------------------------------------------------------------------------

## ðŸš€ How to Run the Workflow

This workflow uses **manual dispatch** (`workflow_dispatch`).

1.  Open your GitHub repository
2.  Go to the **Actions** tab
3.  Select **Build Godot Android Template**
4.  Click **Run workflow**
5.  Press the green **Run workflow** button

â³ Build time is usually **30--60 minutes** depending on GitHub runner
availability.

------------------------------------------------------------------------

## ðŸ“¦ Build Outputs (Artifacts)

After a successful run, download artifacts from the workflow summary
page:

### ðŸ“ android-export-templates

-   Contains the generated Android **export template APKs**
-   Includes **arm32** and **arm64** builds

### ðŸ“ android_source

-   Contains `android_source.zip`
-   Required when using **"Use Custom Build"** in Godot Android export
    settings

------------------------------------------------------------------------

## âš™ Workflow Configuration Details

  Component       Value
  --------------- ------------------------------------
  Godot Version   Latest Stable (autoâ€‘detected)
  Java            Temurin JDK 17
  Android SDK     API 35
  Android NDK     28.1.13356709
  Build Tool      SCons 4.0+
  Encryption      AESâ€‘256 (optional but recommended)

------------------------------------------------------------------------

## âš  Troubleshooting

### âŒ Build fails at encryption step

-   Ensure `SCRIPT_AES256_ENCRYPTION_KEY` is:
    -   Exactly **64 hex characters**
    -   Contains **no spaces or newlines**

### âš  Swappy not detected

-   Ensure Swappy static libraries exist at:

```{=html}
<!-- -->
```
    thirdparty/swappy-frame-pacing/
     â”œâ”€â”€ arm64-v8a/libswappy_static.a
     â””â”€â”€ armeabi-v7a/libswappy_static.a

### ðŸ’¾ Disk space issues

-   Android NDK + SCons generates large intermediate files
-   The workflow includes cleanup steps, but failed jobs may need a
    reâ€‘run

------------------------------------------------------------------------

## ðŸ“ Notes

-   You may pin a specific Godot version by editing the workflow
    checkout step
-   Selfâ€‘hosted runners are recommended for faster builds
-   Artifacts can be uploaded to GitHub Releases if desired

------------------------------------------------------------------------

## ðŸ“„ License

Add your repository license here.
