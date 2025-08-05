# Use a standard Ubuntu image as our base
FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Install necessary packages for VNC, a lightweight window manager, and Flutter
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    openjdk-11-jdk \
    libgtk-3-0 \
    libglu1-mesa \
    xvfb \
    x11vnc \
    fluxbox \
    wget \
    unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Download and install Flutter SDK
ARG FLUTTER_VERSION="3.13.9"
RUN wget https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_${FLUTTER_VERSION}-stable.tar.xz -O /tmp/flutter.tar.xz \
    && tar -xf /tmp/flutter.tar.xz -C /opt/ \
    && rm /tmp/flutter.tar.xz
ENV PATH="/opt/flutter/bin:${PATH}"

# Accept Flutter licenses
RUN flutter doctor --android-licenses

# Set up a non-root user
RUN useradd -ms /bin/bash vscode
USER vscode
WORKDIR /home/vscode

# Set up VNC password
RUN mkdir -p /home/vscode/.vnc && echo "vscode" | vncpasswd -f > /home/vscode/.vnc/passwd && chmod 600 /home/vscode/.vnc/passwd

# Expose VNC port
EXPOSE 5901
