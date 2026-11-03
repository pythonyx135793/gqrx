FROM ubuntu:24.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -qq && apt-get install -y \
    cmake g++ make libboost-dev libpulse-dev portaudio19-dev libsndfile-dev \
    liblog4cpp5-dev gnuradio-dev gr-osmosdr liborc-0.4-dev \
    qt6-base-dev libqt6svg6-dev libqt6svgwidgets6 libgl-dev
COPY . /src
WORKDIR /src
RUN mkdir build-pulse && cd build-pulse \
    && cmake -DLINUX_AUDIO_BACKEND:STRING=Pulseaudio -DBUILD_TESTS=ON .. \
    && make -j$(nproc) \
    && ctest --output-on-failure
RUN mkdir build-gr && cd build-gr \
    && cmake -DLINUX_AUDIO_BACKEND:STRING=Gr-audio .. \
    && make -j$(nproc)
