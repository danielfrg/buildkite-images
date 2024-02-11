FROM buildkite/agent:3-ubuntu
ARG ARCH=x86_64

RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gh \
    gnupg \
    jq \
    unzip

# Install awscli
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && ./aws/install

# Install rye
RUN curl -L -O https://github.com/mitsuhiko/rye/releases/latest/download/rye-$ARCH-linux.gz \
    && gunzip rye-${ARCH}-linux.gz \
    && chmod +x ./rye-${ARCH}-linux \
    && mv ./rye-${ARCH}-linux /usr/local/bin/rye \
    && rm -rf rye-${ARCH}-linux.gz

RUN rye self install --yes

RUN echo 'source "$HOME/.rye/env"' >> ~/.bashrc
