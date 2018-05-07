FROM prsam/phylanx_images:hpx-debug

RUN apt-get update  &&                                                           \
    apt-get -y install wget &&                                                   \
    apt-get -y install python3 python3-dev python3-pip &&                        \
    apt-get -y install libblas-dev liblapack-dev &&                              \
    apt-get -y install libhdf5-dev &&                                            \
    pip3 install setuptools &&                                                   \
    pip3 install pytest &&                                                       \
    pip3 install numpy &&                                                        \
    pip3 install flake8 &&                                                       \
    cd / &&                                                                      \
    git clone --depth=1 https://github.com/pybind/pybind11.git pybind11-src &&   \
    cd pybind11-src &&                                                           \
    mkdir build && cd build &&                                                   \
    cmake  -DPYBIND11_TEST=OFF .. &&                                             \
    make install &&                                                              \
    cd / &&                                                                      \
    rm -rf /pybind11-src &&                                                      \
    git clone --depth=1 https://bitbucket.org/blaze-lib/blaze.git blaze-src &&   \
    cd blaze-src &&                                                              \
    mkdir build && cd build &&                                                   \
    cmake -DBLAZE_SMP_THREADS=C++11 .. &&                                        \
    make install &&                                                              \
    cd / &&                                                                      \
    rm -rf /blaze-src  &&                                                        \
    git clone --depth=1 https://github.com/BlueBrain/HighFive.git highfive-src &&\
    cd highfive-src &&                                                           \
    mkdir build && cd build &&                                                   \
    cmake -DUSE_BOOST=Off .. &&                                                  \
    make install &&                                                              \
    cd / &&                                                                      \
    rm -rf /highfive-src

RUN git clone --depth=1 https://github.com/STEllAR-Group/phylanx /phylanx
RUN mkdir /phylanx/build
RUN cd phylanx/build && cmake -DCMAKE_BUILD_TYPE=Debug -DPHYLANX_WITH_GIT_COMMIT=$(git rev-parse HEAD) -DPHYLANX_WITH_TOOLS=On -DHPX_DIR=/usr/local/lib/cmake/HPX -Dblaze_DIR=/blaze/share/blaze/cmake -DPHYLANX_WITH_HIGHFIVE=On ..
RUN make -C /phylanx/build -j20 tools.inspect
RUN make -C /phylanx/build -j20
RUN make -C /phylanx/build -j20 install
RUN rm -rf /phylanx/build

RUN ldconfig
