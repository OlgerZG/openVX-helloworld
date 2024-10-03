Sample 1 - Build OpenVX 1.3 on Ubuntu 18.04

    Git Clone project with recursive flag to get submodules

git clone --recursive https://github.com/KhronosGroup/OpenVX-sample-impl.git

    Use Build.py script

cd OpenVX-sample-impl/
python Build.py --os=Linux --arch=64 --conf=Debug --conf_vision --enh_vision --conf_nn
or 
python3 Build.py --os=Linux --arch=64 --conf=Debug --conf_vision --enh_vision --conf_nn

### Build and run conformance

export OPENVX_DIR=$(pwd)/install/Linux/x64/Debug
export VX_TEST_DATA_PATH=$(pwd)/cts/test_data/
mkdir build-cts
cd build-cts
cmake -DOPENVX_INCLUDES=$OPENVX_DIR/include -DOPENVX_LIBRARIES=$OPENVX_DIR/bin/libopenvx.so\;$OPENVX_DIR/bin/libvxu.so\;pthread\;dl\;m\;rt -DOPENVX_CONFORMANCE_VISION=ON -DOPENVX_USE_ENHANCED_VISION=ON -DOPENVX_CONFORMANCE_NEURAL_NETWORKS=ON ../cts/
cmake --build .
LD_LIBRARY_PATH=./lib ./bin/vx_test_conformance


### INstalling 
Packaging: After a successful build, you can find the packaged implementation in:
out/LINUX/x86_64/openvx-*.deb

which can be installed using:
dpkg-deb -i <path>/openvx-*.deb


## How to build main 
g++ -o main main.cpp `pkg-config --cflags --libs opencv4` \
-I ./OpenVX-sample-impl/install/Linux/x64/Debug/include/ \
-L ./OpenVX-sample-impl/install/Linux/x64/Debug/bin \
-lopenvx -lopencv_core -lopencv_highgui -lopencv_imgproc

export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:./OpenVX-sample-impl/install/Linux/x64/Debug/bin

./main

# SRC OpenVX examples
https://github.com/KhronosGroup/openvx-samples/tree/main
### goal: /canny-edge-detector/
