FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Dipendenze di sistema
RUN apt-get update && apt-get install -y \
    curl \
    git \
    unzip \
    xz-utils \
    zip \
    libglu1-mesa \
    libgtk-3-dev \
    clang \
    cmake \
    ninja-build \
    pkg-config \
    openjdk-17-jdk \
    && rm -rf /var/lib/apt/lists/*

# Installazione Flutter
RUN git clone https://github.com/flutter/flutter.git /opt/flutter

ENV PATH="/opt/flutter/bin:/opt/flutter/bin/cache/dart-sdk/bin:${PATH}"

# Pre-cache (evita download dopo)
RUN flutter doctor
