# studiorack-template-juce
![Release](https://github.com/studiorack/studiorack-template-juce/workflows/Release/badge.svg)

Audio plugin starter template using JUCE framework to build binaries using:

* Bash
* CMake 3.15.x
* JUCE 6.0.x

This repo demonstrates two ways to build JUCE plugins:

1. cmake: ./.github/workflows/release.yml
2. Projucer ./.github/workflows/release_projucer.yml

## Installation

Install CMake and Xcode using:

    brew install cmake
    xcode-select --install

Check you have the correct dependencies installed:

    cmake -version
    xcodebuild -version

Ensure all git submodules are initialized:

    git submodule update --init --recursive


## Usage

Make all your plugin development changes in the source folder at:

    ./src

Ensure you also update the preview image and audio files:

    ./src/assets/name.png
    ./src/assets/name.wav


## Testing your plugin

Todo


## Build (manual)

Depending on the the operating system you are on/building for, swap the generator string in the build commands:

* Linux: "Unix Makefiles"
* MacOS: "Xcode"
* Windows: "Visual Studio 16 2019"

Compile a development version of the plugin using:

    cmake \
      -G "Xcode" \
      -DCMAKE_BUILD_TYPE=Debug \
      -DJUCE_BUILD_EXAMPLES=ON \
      -DJUCE_BUILD_EXTRAS=OFF \
      -S ./jucesdk \
      -B ./build
    cmake --build ./build --config Debug --target AudioPluginExample_All

View the built plugin files at:

    ./build/examples/CMake/AudioPlugin/AudioPluginExample_artefacts/Debug/VST3

Build the final plugin binaries using:

    cmake \
      -G "Xcode" \
      -DCMAKE_BUILD_TYPE=Release \
      -DJUCE_BUILD_EXAMPLES=ON \
      -DJUCE_BUILD_EXTRAS=OFF \
      -S ./jucesdk \
      -B ./build
    cmake --build ./build --config Release --target AudioPluginExample_All

Rename file if it contains invalid characters/spaces:

    mv "./build/examples/CMake/AudioPlugin/AudioPluginExample_artefacts/Release/VST3/Audio Plugin Example.vst3" ./build/examples/CMake/AudioPlugin/AudioPluginExample_artefacts/Release/VST3/audio-plugin-example.vst3

Copy any additional files:

    cp -v ./src/assets/* ./build/examples/CMake/AudioPlugin/AudioPluginExample_artefacts/Release/VST3

For metadata generation as json use the studiorack-cli:

    npm install @studiorack/cli -g

Validate your plugin:

    studiorack validate "./build/examples/**/*.{vst,vst3}"

Convert and enrich validator report metadata into json:

    studiorack validate "./build/examples/**/*.{vst,vst3}" --json


## Build (automatic)

Release a plugin version on GitHub by simply creating a version tag:

    git tag v0.0.1
    git push && git push origin --tags

This will run an automated build and release process on GitHub Actions:

    .github/workflows/release.yml


## Resources & guides

* [JUCE framework source code and examples](https://github.com/juce-framework/JUCE)
* [Official JUCE guide to creating VST audio plugins](https://juce.com/learn/tutorials)


## Contact

For more information please contact kmturley
