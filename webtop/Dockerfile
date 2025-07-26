# Base Image: The official linuxserver.io webtop
FROM lscr.io/linuxserver/webtop:ubuntu-xfce

# Set environment variables for non-interactive installations
ENV DEBIAN_FRONTEND=noninteractive

# Switch to root user for system-wide installations
USER root

# --- Install System Prerequisites and Applications ---
# Install core dependencies as root
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        wget \
        gpg \
        software-properties-common \
        ca-certificates \
        apt-transport-https \
        vlc \
        libreoffice \
        python3 \
        python3-pip \
        pipx \
        ffmpeg \
        unzip \
        zip \
        nano \
        vim-gtk3 \
        build-essential \
        htop && \
    \
    # Install Python packages globally as root [not recommended as heavy on space]
    # python3 -m pip install -U --break-system-packages \
    #     yt-dlp \
    #     markitdown-mcp \
    #     pandas \
    #     numpy \
    #     flask \
    #     flask_cors \
    #     requests && \
    # \
    # VS Code Installation (Repository handles latest)
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /usr/share/keyrings/packages.microsoft.gpg && \
    echo "deb [arch=amd64,arm64,armhf signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list && \
    \
    # Google Chrome Installation (Direct URL often gets latest)
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb -O /tmp/google-chrome-stable_current_amd64.deb && \
    \
    # Obsidian Installation (Manually update version or use dynamic method)
    # As of July 26, 2025, the latest stable desktop release of Obsidian is 1.8.10.
    wget https://github.com/obsidianmd/obsidian-releases/releases/download/v1.8.10/obsidian_1.8.10_amd64.deb -O /tmp/obsidian_latest_amd64.deb && \
    \
    # OBS Studio PPA addition (Repository handles latest)
    add-apt-repository -y ppa:obsproject/obs-studio && \
    \
    # Second apt-get update after adding repos
    apt-get update && \
    \
    # Install VS Code, Google Chrome, Obsidian, OBS Studio
    apt-get install -y \
        code \
        /tmp/google-chrome-stable_current_amd64.deb \
        /tmp/obsidian_latest_amd64.deb \
        obs-studio && \
    \
    # Cleanup downloaded .deb files (performed as root)
    rm /tmp/google-chrome-stable_current_amd64.deb \
       /tmp/obsidian_latest_amd64.deb 
    #bought from prev line    && \
    # \
    # # Final cleanup to reduce image size significantly
    # apt-get autoremove -y && \
    # apt-get clean && \
    # rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Switch to the non-root user (typically 'abc' in linuxserver.io images)
# USER abc

# Reset DEBIAN_FRONTEND (optional)
ENV DEBIAN_FRONTEND=dialog