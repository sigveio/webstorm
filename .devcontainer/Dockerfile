FROM node:lts-bullseye
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
     && apt-get -y install --no-install-recommends curl zsh gcc g++ make \
     ruby-full ruby-dev libssl-dev libreadline-dev zlib1g-dev \
     autoconf bison build-essential libyaml-dev libreadline-dev \
     libncurses5-dev libffi-dev libgdbm-dev nano vim
USER node
RUN mkdir /home/node/dev
ENV NPM_CONFIG_PREFIX=/home/node/.pkg-global
ENV PATH=$PATH:$NPM_CONFIG_PREFIX/bin
RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
RUN git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
RUN echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
RUN curl -fsSL https://github.com/rbenv/rbenv-installer/raw/HEAD/bin/rbenv-installer | bash
COPY --chown=node:node dotfiles/.zshrc /home/node
COPY --chown=node:node dotfiles/.p10k.zsh /home/node
RUN echo 'eval "$(rbenv init -)"' >> ~/.zshrc
ENV PATH="/home/node/.rbenv/bin:$PATH"
RUN export PATH="$(yarn global bin):$PATH"
RUN rbenv install 2.7.6
RUN rbenv global 2.7.6
#SHELL ["/usr/bin/zsh"]
#RUN gem install bundler
#RUN gem install shopify_transporter
