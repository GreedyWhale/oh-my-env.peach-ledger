FROM madao1994/oh-my-docker:base

WORKDIR /root/repos

RUN apt-get update
# 不安装 libpq-dev 会导致 Could not find gem 'pg (~> 1.1)' in locally installed gems. 的报错
RUN apt-get install -y gnupg2 libpq-dev

# 安装rvm
RUN gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
RUN /bin/zsh -c 'curl -sSL https://get.rvm.io | bash -s stable'
# 修改rvm源为国内镜像
RUN echo "ruby_url=https://cache.ruby-china.com/pub/ruby" > /usr/local/rvm/user/db
RUN echo 'source /usr/local/rvm/scripts/rvm' >> ~/.zshrc
RUN /bin/zsh -c "source ~/.zshrc"

# see https://stackoverflow.com/questions/25899912/how-to-install-nvm-in-docker/60137919#60137919
SHELL ["/bin/zsh", "--login", "-i", "-c"]
# 安装Node
RUN nvm install --lts
RUN nvm use --lts
RUN corepack enable

# 安装Ruby
# see https://stackoverflow.com/a/72216805
RUN rvm install ruby-3.1.2
RUN rvm --default use ruby-3.1.2

# 修改gem和bundle源为国内源
RUN gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
RUN bundle config mirror.https://rubygems.org https://gems.ruby-china.com
RUN gem update --system
# see： https://teratail.com/questions/614nlzx9v4oa4l
RUN gem install rails bundler

# 为了让 vscode 默认使用 zsh
ENV SHELL /bin/zsh
SHELL ["/bin/zsh", "--login", "-c"]
