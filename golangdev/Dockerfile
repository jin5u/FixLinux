FROM ubuntu:20.04

ENV GOPATH="/go" PATH="/go/bin:/usr/local/go/bin:$PATH:/usr/local/node/bin:/usr/local/nvim-linux64/bin" TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone &&\
apt update &&\
apt install -y --no-install-recommends telnet dnsutils mercurial build-essential curl git m4 texinfo libbz2-dev libcurl4-openssl-dev libexpat1-dev libncurses-dev zlib1g-dev zip unzip locales xfonts-utils fontconfig universal-ctags cmake libc6-dev pkg-config libelf1 wget iputils-ping software-properties-common ninja-build gettext libtool libtool-bin autotools-dev automake sudo python3-pip python3-setuptools openssh-client supervisor nginx tmux screen openssh-server ack python3-dev &&\
mkdir /go && mkdir -p /var/run/sshd && chmod 0755 /var/run/sshd &&\
wget https://nodejs.org/dist/v18.12.1/node-v18.12.1-linux-x64.tar.xz && tar xf node-v18.12.1-linux-x64.tar.xz && mv node-v18.12.1-linux-x64 /usr/local/node && rm node-v18.12.1-linux-x64.tar.xz && \
wget https://github.com/krallin/tini/releases/download/v0.19.0/tini-amd64 -O /bin/tini && chmod +x /bin/tini &&\
wget https://github.com/neovim/neovim/releases/download/v0.8.1/nvim-linux64.tar.gz && tar -C /usr/local -xzf nvim-linux64.tar.gz && rm nvim-linux64.tar.gz && \
curl -fsSL "https://dl.google.com/go/go1.19.3.linux-amd64.tar.gz" -o golang.tar.gz \
        && echo "74b9640724fd4e6bb0ed2a1bc44ae813a03f1e72a4c76253e2d5c015494430ba golang.tar.gz" | sha256sum -c - \
        && tar -C /usr/local -xzf golang.tar.gz \
        && rm golang.tar.gz &&\
curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim &&\
curl -Ssl https://raw.githubusercontent.com/jin5u/FixLinux/master/dotfile/.vimrc -o ~/.vimrc &&\
curl -Ssl https://raw.githubusercontent.com/jin5u/FixLinux/master/dotfile/.bashrc -o ~/.bashrc &&\
mkdir -p ~/.config && mkdir -p /root/.vim/ &&\
ln -s /root/.vim /root/.config/nvim &&\
ln -s /root/.vimrc /root/.vim/init.vim &&\
curl -Ssl https://raw.githubusercontent.com/jin5u/FixLinux/master/dotfile/coc-settings.json -o /root/.config/nvim/coc-settings.json &&\
mkdir -p ~/.vim/colors/ &&\
npm install --global yarn &&\
npm install -g neovim &&\
pip3 install neovim --upgrade && nvim -i NONE -c PlugInstall! -c quitall &&\
nvim +GoInstallBinaries +qall &&\
echo "en_US.UTF-8 UTF-8" > /etc/locale.gen &&\
locale-gen "en_US.UTF-8"&& mkdir ~/.fonts/ &&\
cd ~/.fonts/ &&\
git clone https://github.com/eugeii/consolas-powerline-vim.git &&\
cd consolas-powerline-vim/ &&\
cp *.ttf .. &&\
cd .. &&\
rm -rf consolas-powerline-vim/ &&\
mkfontscale &&\
mkfontdir &&\
fc-cache -vf

ENTRYPOINT ["/bin/tini", "--"]
CMD ["/usr/bin/sleep", "200d"]
