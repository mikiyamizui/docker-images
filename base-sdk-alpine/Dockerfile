FROM mikiyamizui/base-alpine

ARG USERNAME=dev
ARG USER_UID=1000
ARG USER_GID=${USER_UID}

RUN apk update \
    && apk add --no-cache sudo less git vim fish

RUN sed -i -e 's;root:/bin/ash$;root:/sbin/nologin;g' /etc/passwd \
    && addgroup -g ${USER_GID} -S ${USERNAME} \
    && adduser -s $(which fish) -G ${USERNAME} -D -S ${USERNAME} \
    && echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME} \
    && sed -i -e "s;/bin/ash;$(which fish);g" /etc/passwd

USER ${USERNAME}
SHELL [ "/usr/bin/fish", "-c" ]
COPY --chown=${USERNAME}:${USERNAME} ./dotfiles /home/${USERNAME}
RUN curl https://git.io/fisher --create-dirs -sLo ~/.config/fish/functions/fisher.fish \
    && fisher add \
    fishpkg/fish-git-util \
    joseluisq/gitnow@2.1.1 \
    rafaelrinaldi/pure

ENV USER ${USERNAME}
ENV HOME /home/${USER}
