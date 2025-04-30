
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# # Install required system packages
RUN apt-get update && apt-get install -y \
    git \
    ruby \
    ruby-dev \
    bundler \
    build-essential \
    p7zip-full \
    innoextract \
    upx \
    curl \
    unzip \
    python3-pip \
    binwalk \
    gcc \
    file \
    binutils \
    wget \
    && pip3 install uefi_firmware \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /opt/tools

RUN wget -q https://github.com/LongSoft/UEFITool/releases/download/A71/UEFIFind_NE_A71_x64_linux.zip && \
    wget -q https://github.com/LongSoft/UEFITool/releases/download/A71/UEFITool_NE_A71_x64_linux.zip && \
    wget -q https://github.com/LongSoft/UEFITool/releases/download/A71/UEFIExtract_NE_A71_x64_linux.zip && \
    unzip -d UEFIFindDir UEFIFind_NE_A71_x64_linux.zip && \
    unzip -d UEFIToolDir UEFITool_NE_A71_x64_linux.zip && \
    unzip -d UEFIExtractDir UEFIExtract_NE_A71_x64_linux.zip && \
    mv UEFIFindDir/uefifind* ./uefifind && \
    mv UEFIToolDir/uefitool* ./uefitool && \
    mv UEFIExtractDir/uefiextract* ./uefiextract && \
    rm *.zip && rm -rf UEFIFindDir UEFIToolDir UEFIExtractDir && \
    ln -s /opt/tools/uefifind /usr/local/bin/UEFIFind && \
    ln -s /opt/tools/uefitool /usr/local/bin/UEFITool && \
    ln -s /opt/tools/uefiextract /usr/local/bin/uefiextract

# # Clone and build rom-parser
WORKDIR /opt
RUN git clone https://github.com/awilliam/rom-parser.git /opt/rom-parser && \
     cd /opt/rom-parser && make && cp rom-parser /usr/local/bin

# # Clone and set up VBiosFinder
RUN git clone https://github.com/coderobe/VBiosFinder.git
WORKDIR /opt/VBiosFinder
RUN bundle install 
WORKDIR /opt/VBiosFinder