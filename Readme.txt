Two packages have to be installed for Android, named Android SDK and Android NDK, Android SDK may now be a part of Android Studio, they are also available for the open source Replicant OS and LineageOS. Download them and put them in some directory so you know where they are. Android NDK should be stable version r14b or later. Android SDK also provides a full graphical Android emulator, which can be configured and started by running android in the tools directory. Android NDK and the tools directory of the Android SDK have to be in path, like add the following to the ~/.profile, but they will be added to path only after restarting the computer.

export PATH=$PATH:/usr/local/programs/replicant-sdk_linux-x86/tools
export PATH=$PATH:/usr/local/programs/android-ndk-r14b

Also download the source packages of SDL2, SDL_ttf, SDL_image and SDL_mixer, add the links to their directories to the example's directory jni, with names SDL, SDL_ttf, SDL_image and SDL_mixer, and external/smpeg2-2.0.0 in the SDL_mixer source code package, with the name smpeg2 (also other libraries used in SDL_mixer if smpeg2 is not the only one). It is important not to compile them, as their ./configure scripts have bugs which damage them in regard of using them with Android. In the Android.mk file of the SDL_mixer source code, replace all ?= true  with  := false , except for smpeg2 with  := true , if you you don't need them and don't add them to the project as modules.

For making the apk file for Android, go to the example's directory and run on the command line

ant debug install

Add the install there only when the Android emulator is running, then it also installs the apk in the emulator.

