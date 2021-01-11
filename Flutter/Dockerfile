# Base image
FROM ubuntu

# Prerequisites
RUN apt-get update && apt-get install -y \
    curl git unzip xz-utils zip libglu1-mesa wget openjdk-8-jdk
# openjdk-8-jdk is required by android sdk

# Setup new user
RUN useradd -ms /bin/bash developer
# -s choose shell -m create user home directory
USER developer
WORKDIR /home/developer

# Prepare Android
RUN mkdir -p Android/Sdk && cd Android/Sdk && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-6858069_latest.zip && \
    unzip commandlinetools-linux-6858069_latest.zip && \
    rm commandlinetools-linux-6858069_latest.zip && echo "finish rm"

# Setup Android
ENV ANDROID_SDK_ROOT /home/developer/Android/Sdk
RUN cd Android/Sdk && mkdir tools && mv cmdline-tools/* ./tools/ && mv tools/ cmdline-tools/ && \
    cd cmdline-tools//tools/bin && yes | ./sdkmanager --licenses && echo "finish licences" &&\
    ./sdkmanager "build-tools;30.0.3" "platforms;android-30" "sources;android-30" 
    #"platform-tools;30.0.5" "patcher;v4"
    # from the warning seems like sources will install patcher and platform-tools already

# Download just the stable version of Flutter SDK from repo
RUN git clone  -b stable --depth 1 https://github.com/flutter/flutter.git

# Add the flutter tool to your path
ENV PATH "$PATH:/home/developer/flutter/bin"

# Run basic check to download Dark SDK
RUN flutter doctor && flutter config --no-analytics