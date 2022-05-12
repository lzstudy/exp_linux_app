WSL环境配置
========================================

1 换源(阿里源)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 修改源选择文件
::

    sudo vi /etc/apt/sources.list
    sudo apt-get update
    sudo apt-get upgrade
- source.list 阿里源
::

    deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
    deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
    deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
    deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
    deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

2 配置git
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 配置用户信息
::

    git config --global user.name "zw"
    git config --global user.email zw@example.com

- 配置SSH
::

    # 生成SSH, 执行后一直回车
    ssh-keygen -t rsa -C "这里换上你的邮箱"

    # 查看公钥, 该公钥可以用来gitlab/github等身份认证(免密下载等)
    cat ~/.ssh/id_rsa.pub

- 配置缩写
::

    vi ~/.gitconfig
::

    [.gitconfig]
    ================

    [user]
            name = zw
            email = zw@example.com

    [alias]
            br = branch
            st = status
            co = checkout
            pl = pull
            ps = push
            ci = commit
            cp = cherry-pick
- 终端显示分支名
::

    sudo vi ~/.bashrc   # 在结尾追加如下内容
    sources ~/.bashrc
::

    [.bashrc]
    ================
    
    ###################################### ZW APPEND ######################################
    # Show git branch name
    force_color_prompt=yes
    color_prompt=yes

    parse_git_branch() {
        git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
    }
    if [ "$color_prompt" = yes ]; then
        PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
    else
        PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w$(parse_git_branch)\$ '
    fi
    unset color_prompt force_color_prompt

3 配置vim
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 配置基本功能
::

    cp /etc/vim/vimrc ~/.vimrc
    vi ~/.vimrc

- vimrc中添加如下内容
::

    if has("autocmd")
        au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif
    endif

    set number              " Show line number

