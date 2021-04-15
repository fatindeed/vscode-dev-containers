# [Choice] Go version: 1, 1.16, 1.15
ARG VARIANT=1
FROM golang:${VARIANT}

# [Option] Install zsh
ARG INSTALL_ZSH="true"
# [Option] Upgrade OS packages to their latest versions
ARG UPGRADE_PACKAGES="true"
# [Option] Remote user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

ENV GO111MODULE=auto

COPY library-scripts/ /tmp/library-scripts/

RUN set -e; \
    # Install needed packages and setup non-root user. Use a separate RUN statement to add your own dependencies.
    bash /tmp/library-scripts/common-debian.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}" "true" "true"; \
    # Install Go tools
    bash /tmp/library-scripts/go-debian.sh "none" "/usr/local/go" "${GOPATH}" "${USERNAME}" "false"; \
    # Other works
    sudo -u $USERNAME mkdir -p /home/$USERNAME/.vscode-server /home/$USERNAME/.vscode-server-insiders; \
    apt-get clean -y; \
    rm -rf /var/lib/apt/lists/* /tmp/library-scripts;
