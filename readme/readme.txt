2020.07.17
----------
Update to buildroot 2020.05
TF-A: v2.3
OP-TEE: 3.7.0

GIT tag
-------
git tag -m "update to buildroot 2020.05, using FIT Image" V1.1.0
git push --tags

GIT submodul
------------
git pull --recurse-submodules
git submodule update --recursive --remote
cd buildroot
git tag --list | grep 2020
git checkout 2020.05
cd ..
git  commit -m "update to 2020.05" buildroot



