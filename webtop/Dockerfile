# Base Image: The official linuxserver.io webtop
FROM lscr.io/linuxserver/webtop:ubuntu-xfce

# Switch to root user for system-wide installations
USER root

# --- Install System Prerequisites ---
# Install tools needed for adding repositories and downloading packages
# Use --no-install-recommends to keep the image lean
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    wget \
    gpg \
    software-properties-common \
    ca-certificates \
    apt-transport-https

# --- Install Applications ---

# --- Visual Studio Code ---
# 1. Add Microsoft's GPG key
# 2. Add the official VS Code repository
# 3. Install VS Code
RUN wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /usr/share/keyrings/packages.microsoft.gpg && \
    echo "deb [arch=amd64,arm64,armhf signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list && \
    apt-get update && \
    apt-get install -y code

# --- Google Chrome ---
# 1. Download the official .deb package
# 2. Install it using apt to handle dependencies
# 3. Clean up the downloaded file
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
    apt-get install -y ./google-chrome-stable_current_amd64.deb && \
    rm google-chrome-stable_current_amd64.deb

# --- Obsidian ---
# 1. Download the latest .deb package from GitHub
# 2. Install it using apt
# 3. Clean up the downloaded file
RUN wget https://github.com/obsidianmd/obsidian-releases/releases/download/v1.5.12/obsidian_1.5.12_amd64.deb && \
    apt-get install -y ./obsidian_1.5.12_amd64.deb && \
    rm obsidian_1.5.12_amd64.deb

# --- OBS Studio ---
# 1. Add the official PPA repository
# 2. Install OBS Studio
RUN add-apt-repository -y ppa:obsproject/obs-studio && \
    apt-get update && \
    apt-get install -y obs-studio

# --- VLC Media Player & LibreOffice ---
# Install directly from Ubuntu's repositories
RUN apt-get update && apt-get install -y --no-install-recommends vlc libreoffice

# --- Run Python3-Pip install
RUN apt-get install -y python3-pip
RUN apt-get install pipx -y
RUN apt-get install gh -y

# --- Final Cleanup ---
# Clean up apt cache to reduce image size
RUN rm -rf /var/lib/apt/lists/*

# --- Install Development Tools (as before) ---
# Switch to the standard user for user-specific installations
#USER abc

# Install pipx for the user and add its bin directory to the PATH
#RUN python3 -m pip install --user pipx
#ENV PATH="/home/abc/.local/bin:$PATH"

# Now install python tools using the user's pipx
#RUN pipx install yt-dlp && \
#    pipx install markitdown-mcp

# Install Node.js using nvm and run playwright install in the same layer
# This is the robust way to do it in a Dockerfile
#RUN mkdir -p "$HOME/.nvm"
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
RUN . "nvm.sh" && nvm install --lts

RUN apt-get update && apt-get install -y --no-install-recommends \
    vim-gtk3 \
    nano \
    ffmpeg \
    unzip \
    build-essential \
    zip \
    g++ \
    gcc \
    git \
    curl \
    wget \
    nasm \
    yasm \
    libgtk-3-dev \
    clang \
    libxcb-randr0-dev \
    libxdo-dev \
    libxfixes-dev \
    libxcb-shape0-dev \
    libxcb-xfixes0-dev \
    libasound2-dev \
    libpulse-dev \
    cmake \
    make \
    libclang-dev \
    ninja-build \
    libgstreamer1.0-dev \
    libgstreamer-plugins-base1.0-dev \
    libpam0g-dev \
    && rm -rf /var/lib/apt/lists/*

# DOWNLOAD and INSTALL the RustDesk .deb package
ARG RUSTDESK_VERSION=1.4.1 # You can override this at build time

RUN wget "https://github.com/rustdesk/rustdesk/releases/download/${RUSTDESK_VERSION}/rustdesk-${RUSTDESK_VERSION}-x86_64.deb" \
    && apt-get install -y ./rustdesk-${RUSTDESK_VERSION}-x86_64.deb \
    && rm ./rustdesk-${RUSTDESK_VERSION}-x86_64.deb # Clean up the .deb file


# Install TypeScript globally using npm (requires Node.js to be installed and configured)
#RUN npm install -g typescript