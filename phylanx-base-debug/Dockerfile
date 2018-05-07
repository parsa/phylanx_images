FROM prsam/hpx_auto:master-debug

RUN apt-get update &&                                                                   \
    apt-get install --yes --no-install-recommends                                       \
                python3                                                                 \
                python3-dev                                                             \
                python3-pip                                                             \
                libblas-dev                                                             \
                liblapack-dev                                                           \
                libhdf5-dev &&                                                          \
    apt-get purge && apt-get clean && rm -rf /var/lib/apt/lists/*                    && \
                                                                                        \
    pip3 --no-cache-dir install setuptools                                           && \
    pip3 --no-cache-dir install pytest                                               && \
    pip3 --no-cache-dir install numpy                                                && \
    pip3 --no-cache-dir install flake8                                               && \
                                                                                        \
    git clone --depth=1 https://github.com/pybind/pybind11.git /pybind11             && \
    mkdir -p /pybind11/build                                                         && \
    cd /pybind11/build && cmake -DCMAKE_BUILD_TYPE=Release -DPYBIND11_TEST=OFF ..    && \
    make -C /pybind11/build install                                                  && \
    rm -rf /pybind11                                                                 && \
                                                                                        \
    git clone --depth=1 https://bitbucket.org/blaze-lib/blaze.git /blaze             && \
    mkdir -p /blaze/build                                                            && \
    cd /blaze/build && cmake -DCMAKE_BUILD_TYPE=Release -DBLAZE_SMP_THREADS=C++11 .. && \
    make -C /blaze/build install                                                     && \
    rm -rf /blaze                                                                    && \
                                                                                        \
    git clone --depth=1 https://github.com/BlueBrain/HighFive.git /highfive          && \
    mkdir -p /highfive/build                                                         && \
    cd /highfive/build && cmake -DCMAKE_BUILD_TYPE=Release -DUSE_BOOST=Off ..        && \
    make -C /highfive/build install                                                  && \
    rm -rf /highfive