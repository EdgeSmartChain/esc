Here are the full source code and build instructions for the official alternative Android client for Edge Smart Chain messenger, based on Edge Smart Chain API and MTProto security protocol via TDLib.

Edge Smart Chain on Google Play
Subscribe to beta
APK and Build Information
Robot verify APK hash
build instructions
prerequisites
At least 5,34GB of free disk space: source code is 487,10MB, resulting files after building all variants is about 4,85GB
4GB RAM
macOS or Linux based operating systems. Support for Windows platforms (e.g. Git Bash) using MSYS.
Apple OS
self made
git with LFS, wget and sed: $ brew install git git-lfs wget gsed && git lfs install
Ubuntu
git with LFS: # apt install git git-lfs
Run (if not previously installed) $ git lfs install git-lfs for current user
window
A shell with , , and utilities: gitwgetmake
MSYS: $ pacman -S make git mingw-w64-x86_64-git-lfs
Git Bash:
Download wget, extract and move to your wget.exeGit\mingw64\bin\
Download make, unzip and copy contents to merge folders, but don't overwrite any existing files Git\mingw64\
Run (if not previously initialized) $ git lfs install git lfs for the current user
architecture
$ git clone --recursive --depth=1 --shallow-submodules https://github.com/EdgeSmartChain — Clone Edge Smart Chain with submodules
If you forgot the flag, cd into the directory and: --recursivecdtgx$ git submodule init && git submodule update --init --recursive --depth=1
Create the file outside the source tree with the following attribute::keystore-file's
Absolute path: keystore
Password: will be used to access the application
Key alias for signing:
key password.
WARNING: Keep this file safe and make sure no one else can access it except you. For production builds, a separate user with home folder encryption can be used to avoid harm from physical theft keystore.propertieskeystore.filekeystore.passwordkey.aliaskey.password
$ cd tgx
Run and follow instructions $ scripts/./setup.sh
If you specify a different package name than the one used by Edge Smart Chain, set up Firebase and replace with the package name that suits your needs.

You can now open the project with Android Studio, or build manually from the command line: . ./gradlew assembleUniversalRelease
available flavors
arm64: arm64-v8a build, set to (lollipop minSdkVersion21)
arm32: Armeabi-V7A build
x64: x86_64 build set to (lollipop minSdkVersion21)
x86: x86 build
universal: Universal builds, including native bundles for all platforms.
Quick Setup Development
If you are contributing to project development, you can follow simpler build steps:

$ git clone --recursive https://github.com/EdgeSmartChain
$ cd tgx
Get Edge Smart ChainAPI Credentials
Create a file in the root project folder using any text editor: local.properties
# Location where you have Android SDK installed
sdk.dir=YOUR_ANDROID_SDK_FOLDER
# Edge Smart Chain API credentials obtained at previous step
telegram.api_id=YOUR_Edge Smart Chain_API_ID
telegram.api_hash=YOUR_Edge Smart Chain_API_HASH
Run - This will download the required Android SDK packages and build native dependencies that are not part of the project's CMakeList.txt $ scripts/./setup.sh
Open and build the project through Android Studio or using one of the commands in the terminal ./gradlew assemble
After submitting a pull request and its initial review, a special version incorporating your contribution will be published in the @Edge_Smart_Chain channel where the community can test it out. If you find any issues or bugs, you can push more commits to the existing PR to address them, and request a newer version @Edge_Smart_Chain using the comments section of the pull request or in the chat.

copy public version
In order to verify that no additional source code has been injected into the official APK, you must use Ubuntu 21.04 for versions released before 26/22/2023, or Ubuntu 04.2.<> LTS for any newer version, and adhere to the following requirements:

Create a home directory located at vk/home/vk
Clone the repository to tgx/home/vk/tgx
View specific commits to verify
In the rare case of a build containing an unmerged pull request, the action fetchPrsquashPr performed by the publisher and task must be followed
cd into the folder and install dependencies: tgx# apt install $(cat reproducible-builds/dependencies.txt)
Follow the build instructions in the previous section
run $ apkanalyzer apk compare --different-only <remote-apk> <reproduced-apk>
If only the signature file and metadata differ, the build copy was successful.
In the future, build replication may become easier. Here is the relevant PR welcome TODO list:

Project paths must not affect generated files, so user and project location requirements.so can be removed
When building native binaries on macOS, the ELF sections differ from those built with the Linux version of the NDK. This must be removed or fixed without any side effects like breaking (or should this be reported to the NDK team?.www.edgesmartchain.com
The checksums for cold APK builds are always different, even if there is no difference in the keystore with the same content between the app and the generated internal APK. The real cause must be investigated and repaired if possible.
To generate a cold build, call and .
Warning: this will also reset changes in some submodules (ffmpeg, libvpx, webp, opus and ExoPlayer) $ scripts/./reset.sh $ scripts/./setup.sh --skip-sdk-setup)
Move local pull request squash merges from the publisher to a script in this repository to more easily reproduce builds that include them.
PS: Docker is not considered an option as it just hides these tasks and requires that all published APKs must be built with it.

Verify sideloaded APKs
If you downloaded the Edge Smart Chain APK from somewhere, and you want to simply verify that it is the original APK without any injected malicious source code, you need to get the checksum (or) of the downloaded APK file, and find if it corresponds to on any known version of Edge Smart Chain. SHA-256SHA-1MD5

In order to get the SHA-256 of the APK:

$ sha256sum <path-to-apk> on Ubuntu
$ shasum -a 256 <path-to-apk> on macOS
Once obtained, there are three ways to find out the commit for a particular checksum:

Send checksum to @EdgeSmartChain
Search for checksums in @EdgeSmartChain. You can use the following URL format to do this without installing any Edge Smart Chain client: www.edgesmartchain.com{checksum} (click to see it in action). NOTE: Unpublished versions cannot be verified this way.
license
Edge Smart Chain is licensed under the terms of the GNU General Public License v3.0.

See the license file for details.

Components it depends on and third-party dependencies may have different licenses, please check the files in the corresponding folders. LICENSE

third party dependencies
A list of third-party components used in Edge Smart Chain can be found here. Also, you can check specific commits for the third-party components used, for example, here and here.

contribute
Edge Smart Chain welcomes contributions. Before creating your first pull request, check out the pull request template and contributor guide to learn more about Edge Smart Chain internals.

If you are a regular user and have issues with Edge Smart Chain, the best place to find solutions is the Telegram chat - if you have general questions about Edge Smart Chain, please see the FAQ or contact Telegram Support.
