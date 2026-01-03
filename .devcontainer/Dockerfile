FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Dipendenze di base
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
    wget \
    gnupg \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Installazione Google Chrome
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | gpg --dearmor > /usr/share/keyrings/google-linux-keyring.gpg \
    && echo "deb [arch=amd64 signed-by=/usr/share/keyrings/google-linux-keyring.gpg] http://dl.google.com/linux/chrome/deb/ stable main" \
    > /etc/apt/sources.list.d/google-chrome.list \
    && apt-get update \
    && apt-get install -y google-chrome-stable \
    && rm -rf /var/lib/apt/lists/*

# Wrapper Chrome --no-sandbox (QUESTO È IL PUNTO CHIAVE)
RUN echo '#!/bin/bash\nexec google-chrome --no-sandbox "$@"' \
    > /usr/local/bin/chrome-no-sandbox \
    && chmod +x /usr/local/bin/chrome-no-sandbox

# Installazione Flutter
RUN git clone https://github.com/flutter/flutter.git /opt/flutter

ENV PATH="/opt/flutter/bin:/opt/flutter/bin/cache/dart-sdk/bin:${PATH}"

# Pre-cache Flutter
RUN flutter doctor