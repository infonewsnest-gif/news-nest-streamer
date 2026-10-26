name: Build APK
on:
  workflow_dispatch:
  push:
    paths:
      - 'project.zip'
      - '.github/workflows/build.yml'
permissions:
  contents: write
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Unzip project
        run: |
          mkdir work
          unzip -q project.zip -d work
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.9'
      - name: Build
        working-directory: work
        run: gradle assembleDebug --no-daemon --stacktrace
      - name: Release
        uses: softprops/action-gh-release@v2
        with:
          tag_name: build-${{ github.run_number }}
          name: News Nest Live Streamer build ${{ github.run_number }}
          files: work/app/build/outputs/apk/debug/*.apk
