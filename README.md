# 🤖 CI/CD: Android Export Template Builder

This repository includes a GitHub Actions workflow designed to compile custom Godot Android Export Templates from source. This is particularly useful for users who need to include specific modules, custom engine patches, or—as configured here—GDScript encryption.

## 📋 Features

**Automatic Source Fetching:** Clones the latest stable Godot release automatically.

**Architecture Support:** Builds for both `arm32 (v7)` and `arm64 (v8)`.

**Swappy Integration:** Includes the Android Frame Pacing library for smoother rendering.

**Security:** Supports AES256 script encryption to protect your project's source code.

**Artifacts:** Generates both the `.apk` templates and the `android_source.zip` required for Gradle builds.

## 🛠️ Prerequisites

create a new repository and create a `build.yml` file inside `.github/workflows` folder then copy the build code from `build_template.yml` paste it inside the `build.yml` file. 

Navigate to your repository `Settings > Secrets and variables > Actions`

Create a New repository secret.

Name: `SCRIPT_AES256_ENCRYPTION_KEY`

Value: Your 64-character hexadecimal key.

Note: You can generate a key using this website:
https://onecompiler.com/python
and run this code
```python
import os
print(os.urandom(32).hex())

```

Before running the workflow, you must set up your Repository Secret. The workflow is designed to fail early if this key is missing to prevent unencrypted builds.

## 🚀 How to Run
Since this workflow uses the `workflow_dispatch trigger`, it must be started manually:

Go to the Actions tab of this GitHub repository.

Select "Build Godot Android Template" from the sidebar.

Click the Run workflow dropdown and press the green button.

## Video Tutorial 
[![YouTube](https://img.youtube.com/vi/VIDEO_ID/0.jpg)](https://www.youtube.com/watch?v=VIDEO_ID)

