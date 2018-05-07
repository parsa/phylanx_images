FROM prsam/phylanx_images:hpx-release

RUN apt-get update
# Python 3 & Pip
RUN apt-get -y install python3 python3-dev python3-pip
# LAPACK & BLAS
RUN apt-get -y install libblas-dev liblapack-dev
# HDF5
RUN apt-get -y install libhdf5-dev
# SetupTools
RUN pip3 install setuptools
# PyTest
RUN pip3 install pytest
# NumPy
RUN pip3 install numpy
# flake8
RUN pip3 install flake8
# pybind
RUN git clone --depth=1 https://github.com/pybind/pybind11.git /pybind11-src
RUN mkdir -p /pybind11-src/build
RUN cd build && cmake -DCMAKE_BUILD_TYPE=Release -DPYBIND11_TEST=OFF ..
RUN make -C /pybind11-src/build install
RUN rm -rf /pybind11-src
# Blaze
RUN git clone --depth=1 https://bitbucket.org/blaze-lib/blaze.git /blaze-src
RUN mkdir -p /blaze-src/build
RUN cd /blaze-src/build && cmake -DCMAKE_BUILD_TYPE=Release -DBLAZE_SMP_THREADS=C++11 ..
RUN make -C /blaze-src/build install
RUN rm -rf /blaze-src
# HighFive
RUN git clone --depth=1 https://github.com/BlueBrain/HighFive.git /highfive-src
RUN mkdir -p /highfive-src/build
RUN cd /highfive-src/build && cmake -DCMAKE_BUILD_TYPE=Release -DUSE_BOOST=Off ..
RUN make -C /highfive-src/build install
RUN rm -rf /highfive-src

# Phylanx itself
RUN git clone --depth=1 https://github.com/STEllAR-Group/phylanx /phylanx
RUN mkdir /phylanx/build
RUN cd phylanx/build && cmake -DCMAKE_BUILD_TYPE=Release -DPHYLANX_WITH_GIT_COMMIT=$(git rev-parse HEAD) -DPHYLANX_WITH_TOOLS=Off -DHPX_DIR=/usr/local/lib/cmake/HPX -Dblaze_DIR=/blaze/share/blaze/cmake -DPHYLANX_WITH_HIGHFIVE=On ..
RUN make -C /phylanx/build -j20
RUN make -C /phylanx/build -j20 install
RUN rm -rf /phylanx/build

RUN ldconfig
