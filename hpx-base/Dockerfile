FROM debian:stable

RUN apt-get update &&                             \
    apt-get install --yes --no-install-recommends \
                git                               \
                wget                              \
                cmake                             \
                build-essential                   \
                pkg-config                        \
                clang                             \
                libhwloc-dev                      \
                libboost-atomic-dev               \
                libboost-chrono-dev               \
                libboost-date-time-dev            \
                libboost-filesystem-dev           \
                libboost-program-options-dev      \
                libboost-regex-dev                \
                libboost-system-dev               \
                libboost-thread-dev               \
                libjson-perl &&                   \
    apt-get purge && apt-get clean && rm -rf /var/lib/apt/lists/*

ENV CC clang
ENV CXX clang++
