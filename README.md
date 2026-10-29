
name: Build LEFT for Windows

on:
  workflow_dispatch:
  push:
    branches: [main]

jobs:
  build:
    name: Build Windows x64
    runs-on: ubuntu-latest

    steps:
      - name: Download project
        uses: actions/checkout@v4
        with:
          lfs: true

      - name: Build LEFT
        uses: game-ci/unity-builder@v4
        env:
          UNITY_LICENSE: ${{ secrets.UNITY_LICENSE }}
        with:
          targetPlatform: StandaloneWindows64
          buildsPath: build

      - name: Upload Windows build
        uses: actions/upload-artifact@v4
        with:
          name: LEFT-Windows
          path: build
