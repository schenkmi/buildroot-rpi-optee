2024.01.07
----------
Update to buildroot 2023.11
TF-A: v2.7
OP-TEE: 4.0.0

Need to use u-boot 2021.07 due to FIT signature verification issues found in 2022.04
Need to use kernel 967d45b29ca2902f031b867809d72e3b3d623e7a (5.10.1-v8, from 2021.07) due to SD-Card driver issues

2024.01.07
----------
Update to buildroot 2023.02.8
TF-A: v2.7
OP-TEE: 3.19.0

Need to use u-boot 2021.07 due to FIT signature verification issues found in 2022.04
Need to use kernel 967d45b29ca2902f031b867809d72e3b3d623e7a (5.10.1-v8, from 2021.07) due to SD-Card driver issues

2021.03.29
----------
Update to buildroot 2021.02
TF-A: v2.4
OP-TEE: 3.12.0

Updated to OP-TEE OS 3.12.0 as older versions have a issue which gcc-10.x

/work/buildroot-rpi-optee/out/host/bin/aarch64-none-linux-gnu-ld.bfd: /work/buildroot-rpi-optee/out/host/opt/ext-toolchain/bin/../lib/gcc/aarch64-none-linux-gnu/10.2.1/libgcc.a(lse-init.o): in function `init_have_lse_atomics':
/tmp/dgboter/bbs/build04--cen7x86_64/buildbot/cen7x86_64--aarch64-none-linux-gnu/build/src/gcc/libgcc/config/aarch64/lse-init.c:44: undefined reference to `__getauxval'
/work/buildroot-rpi-optee/out/host/aarch64-buildroot-linux-gnu/sysroot/lib/optee/export-ta_arm64/mk/link.mk:109: recipe for target '5b9e0e40-2636-11e1-ad9e-0002a5d5c51b.elf' failed

https://github.com/OP-TEE/optee_os/pull/3874
https://github.com/OP-TEE/optee_os/pull/4154

2020.10.06
----------
Move buildroot external stuff into dedicate folder buildroot-external

2020.09.03
----------
Update to buildroot 2020.08
TF-A: v2.3
OP-TEE: 3.9.0
Remark: need to add core_freq=250 in config.txt for stable serial console

2020.07.17
----------
Update to buildroot 2020.05
TF-A: v2.3
OP-TEE: 3.7.0

GIT submodule and branch
------------------------
If working with a branch we may update the submodule like this
git submodule update --init

GIT tag
-------
git tag -m "update to buildroot 2020.05, using FIT Image" V1.1.0
git push --tags

GIT submodul
------------
git pull --recurse-submodules
git submodule update --recursive --remote
cd buildroot
git tag --list | grep 2023
git checkout 2023.11
cd ..
git  commit -m "update to 2023.11" buildroot

gitk compare tags
-----------------
gitk tags/2020.05..tags/2020.08

update buildroot def config
---------------------------
make update-defconfig

rebuild u-boot (dtb change)
---------------------------
make uboot-dirclean && make uboot

rebuild uboot-env
-----------------
cd out/images
../host/bin/mkenvimage -s 0x4000 -o uboot-env.bin ../../board/rpi3/uboot.env.txt
