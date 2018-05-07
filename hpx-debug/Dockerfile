FROM prsam/phylanx_images:hpx-base

RUN git clone --depth=1 https://github.com/STEllAR-Group/hpx /hpx
RUN mkdir /hpx/build
RUN cd hpx/build && cmake -DCMAKE_BUILD_TYPE=Debug -DHPX_WITH_MALLOC=system -DHPX_WITH_GIT_COMMIT=$(git rev-parse HEAD) -DHPX_WITH_TOOLS=On -DCMAKE_CXX_FLAGS='-fcolor-diagnostics' -DHPX_WITH_TESTS_HEADERS=On -DHPX_WITH_DEPRECATION_WARNINGS=Off -DCMAKE_EXPORT_COMPILE_COMMANDS=On ..
RUN make -C /hpx/build -j20 tools.inspect
RUN make -C /hpx/build -j20
RUN make -C /hpx/build -j20 install
RUN rm -rf /hpx/build

#FROM prsam/hpx:base-devel
#COPY --from=0 /hpx /usr/local/bin/hello_world /usr/local/lib/bazel/hpx* /usr/local/bin/hpx* /usr/local/lib/hpx /usr/local/lib/libhpx* /usr/local/lib/pkgconfig/hpx_* /usr/local/lib/cmake/HPX /usr/local/share/hpx* /usr/local/include/hpx
RUN ldconfig
