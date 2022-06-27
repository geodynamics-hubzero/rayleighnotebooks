FROM ubuntu:22.04

LABEL maintainer <rene.gassmoeller@mailbox.org>

RUN DEBIAN_FRONTEND=noninteractive apt update && apt upgrade -yq && \
  DEBIAN_FRONTEND=noninteractive apt install -yq --no-install-recommends \
  build-essential ca-certificates cmake cmake-curses-gui file gcc g++ \
  gfortran git libblas-dev liblapack-dev libopenmpi-dev \
  lsb-release ninja-build numdiff openmpi-bin \
  openmpi-common wget zlib1g-dev
  
RUN apt install -yq --no-install-recommends libdeal.ii-dev

RUN git clone https://github.com/geodynamics/aspect.git ./aspect && \
    mkdir aspect/build-release && \
    cd aspect/build-release && \
    git checkout main && \
    cmake -DCMAKE_BUILD_TYPE=Release \
          -DASPECT_PRECOMPILE_HEADERS=ON \
          .. && \
    make -j8 && \
    make install
