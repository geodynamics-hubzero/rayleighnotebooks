FROM debian:10

LABEL maintainer <rene.gassmoeller@mailbox.org>

RUN DEBIAN_FRONTEND=noninteractive apt update && apt upgrade -yq && \
  DEBIAN_FRONTEND=noninteractive apt install -yq --no-install-recommends \
  build-essential ca-certificates cmake cmake-curses-gui file gcc g++ \
  gfortran git libblas-dev liblapack-dev libopenmpi-dev \
  lsb-release ninja-build numdiff openmpi-bin \
  openmpi-common wget zlib1g-dev bc
  
COPY local.cfg /opt/

# Install deal.II with minimal dependencies for ASPECT
RUN cd /opt && \
    git clone https://github.com/dealii/candi && \
    cd candi && \
    mv /opt/local.cfg . && \
    ./candi.sh -p /opt -j8 && \
    rm -rf /opt/tmp && \
    ln -s /opt/astyle-2.04/astyle /usr/bin/astyle

ENV DEAL_II_DIR /opt/deal.II-v9.4.0

RUN git clone https://github.com/geodynamics/aspect.git ./aspect && \
    mkdir aspect/build && \
    cd aspect/build && \
    git checkout main && \
    cmake -DCMAKE_BUILD_TYPE=DebugRelease \
          -DASPECT_PRECOMPILE_HEADERS=ON \
          -DASPECT_INSTALL_EXAMPLES=ON \
          .. && \
    make -j8 && \
    make install
