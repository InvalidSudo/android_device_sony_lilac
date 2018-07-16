Device configuration for Sony Xperia XZ1 Compact (lilac)
========================================================

Description
-----------

This repository is for CarbonROM on Sony Xperia XZ1 Compact (lilac).

How to build CarbonROM
----------------------

* Make a workspace:

        mkdir -p ~/bin && mkdir -p ~/CarbonROM

* Install repo:

        curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo && chmod a+x ~/bin/repo

* Initialize the repo:

        cd ~/CarbonROM && repo init -u https://github.com/CarbonROM/android.git -b cr-6.1 && repo sync -f

* Create a local manifest:

        vim .repo/local_manifests/roomservice.xml

        <?xml version="1.0" encoding="UTF-8"?>
        <manifest>
            <!-- SONY -->
            <project name="CarbonROM/android_kernel_sony_msm8998" path="kernel/sony/msm8998" remote="github" />
            <project name="CarbonROM/android_device_sony_common-treble" path="device/sony/common-treble" remote="github" />
            <project name="CarbonROM/android_device_sony_yoshino-common" path="device/sony/yoshino-common" remote="github" />
            <project name="InvalidSudo/android_device_sony_lilac" path="device/sony/lilac" remote="github" />

            <!-- Pinned blobs for lilac -->
            <project name="cryptomilk/android_vendor_sony_lilac" path="vendor/sony/lilac" remote="github" />
        </manifest>

* Sync the repo (again):

        repo sync

* Extract vendor blobs

        cd device/sony/lilac
        ./extract-files.sh

* Setup the environment

        source build/envsetup.sh
        lunch carbon_lilac-userdebug

* Build CarbonROM

        make carbon -j8
