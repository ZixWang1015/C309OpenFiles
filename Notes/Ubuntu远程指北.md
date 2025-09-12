# ubuntu服务器远程使用指北

1. 基本信息：
    - 主机IP地址：xx.xx.xx.xx
    - 主机root用户名：abcdefg
    - root用户密码：hijklmn
    - todesk远程连接编号：xyzxyzxyz
    - todesk连接安全密码：111111

2. 基本使用方法：通过Vscode的SSH远程连接，然后借助终端和命令行即可完成大部分工作
    - Vscode远程连接命令，在Vscode最上方SSH窗口输入：
        ```
        ssh root_name@xx.xx.xx.xx
        ```
    - 为自己添加一个新用户，并赋予sudo权限：
        ```
        sudo -i             # 以管理员身份继续
        adduser abc         # 这里连续两次输入设定密码即可，密码不可见
        adduser abc sudo    # 这里赋予超级管理员权限
        su - abc            # 这里输入密码切换用户
        ```

3. conda环境管理：**请注意不要在自己的用户下重新安装anaconda/miniconda/miniforge**
    - 本机anaconda的安装路径为/opt/anaconda3/bin
    - 添加新用户后，首先借助vim修改其中的环境变量：
        ```
        su - abc
        sudo vim ~/.bashrc
        ```
    - 在自己目录下的.bashrc文件中做修改，全部路径都修改到conda的安装路径：
        ```
        export PATH="/opt/anaconda3/bin:$PATH"
        ```
    - 然后更新.bashrc文件：
        ```
        source ~/.bashrc
        ```
    - 借助source更新.bashrc文件后，若自己用户名前出现(base)字样，即代表环境变量更新完成。
    - 之后与windows一样直接安装自己的conda虚拟环境即可：
        ```
        conda create -n my_env python=3.11.15
        ```
    - 安装特定版本的GPU torch包：
        ```
        pip install torch==2.4.1 -f https://mirrors.aliyun.com/pytorch-wheels/cu124
        ```

4. 内存管理：本机分为/ubuntu(2T)和/data(18T)，尽量把数据都存放在data盘中，包括虚拟环境，模型和数据等。
    - 检查默认的conda安装源和虚拟环境安装路径：
        ```
        conda info
        ```
    - 更改conda默认虚拟环境安装路径：
    - 想要切换到其他盘，先通过命令查看各个存储空间的挂载点：
        ```
        df -h
        ```
    - 然后直接cd到该盘的挂载点上即可，然后通过ls命令查看当前目录，目前默认的环境安装目录在/data盘，可借助下面的命令修改(磁盘的名称与其挂载点一般不同)：
        ```
        conda config --add envs_dirs /mnt/data1/conda_env
        ```
    - 然后安装环境和借助conda env list进行确认
    - 下面获取pip对应的文件位置，更改pip install对应的默认源：
        ```
        pip config -v list
        ```
        需要修改的文件是自己的虚拟环境路径下的那个pip.conf文件，例如我的文件路径在：
        ```
        For variant 'site', will try loading '/mnt/data1/conda_env/my_env/pip.conf'
        ```
        可以借助vim直接再该文件中写入你想要使用的镜像源，如清华源或者阿里云：
        ```
        [global]
        index-url = https://mirrors.aliyun.com/pypi/simple/
        trusted-host = mirrors.aliyun.com
        ```
    - 注意：假设虚拟环境名为abc，当使用conda activate abc时，如果用户显示为
        ```
        (abc) abc@root_user_-Server:~$  # 表明环境安装在/home/wzx/.conda目录下
        ```
        如果用户显示为：
        ```
        (/mnt/data1/conda_env/manyicl) abc@root_user-Server:~$   
        # 表明环境成功安装在/mnt/data1/conda_env/目录下了
        ```

5. 通过Vscode SSH连接Ubuntu创建目录，然后运行python脚本：
    - 先在Vscode的拓展中确定对应的ssh远程控制主机安装了python拓展
    - 然后自动或手动找到自己的虚拟环境，不清楚python位置的话直接在命令行中激活自己的环境：
        ```
        conda activate your_env
        which python
        ```
    - 新建自己的脚本放置的位置：
        ```
        cd /mnt/data1/..
        mkdir ..
    - 如果发现自己在命令行中新建的路径无法在Vscode中直接新建文件，则需要借助sudo指定写的权限：
        ```
        sudo -i
        chmod 777 /mnt/data1/... -R
        ```
    
6. 关于ubuntu中借助huggingface_hub来从huggingface源站，或者modelscope/hf-mirror等站点下载模型：
    - 以下是两个我们经常使用的源站：
        ```
        https://hf-mirror.com/
        https://www.modelscope.cn/home
        ```
    - 然后首先在自己的虚拟环境中安装依赖包：
        ```
        pip install transformers==xx.xx
        pip install huggingface_hub==xx.xx
        ```
    - 更改默认的下载路径为国内镜像，依然是修改.bashrc文件：
        ```
        su - wzx
        vim ~/.bashrc
        + export HF_ENDPOINT="https://hf-mirror.com"
        source ~/.bashrc
        ```
    - 指定好路径，登录huggingface确定好模型名称应该叫什么，之后就可以下载了，注意在下载前cd到合适的路径，免得后面再去复制和删除：
        ```
        huggingface-cli download --resume-download Qwen/Qwen2.5-7B-Instruct --local-dir ./qwen-2.5-7b-instruct
        ```
    - 使用Git来克隆整个repo或者从Github下载单个文件，首先在github页面找到你要下载的文件，例如我这里是https://github.com/TIGER-AI-Lab/LongICLBench/blob/main/processed_data/train_tacred.json，然后注意：点击Github预览框中的“raw”，但是在这里复制链接，因为这里是可以HTML直接交互通过命令行下载文件的。复制好链接后，直接通过命令下载文件：
        ```
        wget https://github.com/TIGER-AI-Lab/LongICLBench/raw/refs/heads/main/processed_data/train_tacred.json
        ```
    


7. 注意事项：
    - 尽量使用命令行，在命令行中移动、删除、新建文件都比GUI中的操作更快。
    - 新用户均需更新~/.bachrc和修改conda config中env_dir和pkg_dir，配合vim进行修改和更新。
    - 新建环境和更新包的时候需注意，自己一定是处于自己的user下，即类似wzx@root123-Rack-Server，不然非root用户或其他用户无法访问该环境。
    - 新用户将环境创建在/mnt/data1/conda_env可能会遇到问题，导致环境自行被创建在/home/user/.conda，可以通过命令检查是否权限不够：
        ```
        ls -ld /mnt/data1/conda_env
        ls -ld /mnt/data1
        ```
    - 借助sudo给与目前用户该路径的读取权限，注意：有时是因为子目录或者父目录中某一个仅赋予了root123用户权限，可以考虑将当前用户添加到root group，或修改当前目录的权限等级：
        ```
        sudo chmod go+x /mnt/data1
        sudo chmod go+x /mnt/data1/conda_env
        ```
        同时注意当前的路径权限的等级：
        ```
        drwxr-xr-x
        drwxrwxr-x
        drwx--x--x
        ```
    - 如果出现在root123用户中nvcc -V可以返回cuda toolkit版本，但是在自己的用户下返回找不到命令，那就说明未正确添加环境变量。环境变量的核心原则是root用户下可以访问的ls应当原封不动的添加到当前的用户的.bashrc文件中，即：
        ```
        su - abc                        # 切换用户
        nvcc -V                         # 返回 找不到命令
        exit                            # 切换回root123用户
        which nvcc                      # 查看nvcc安装在哪个目录
        ls /usr/local/cuda/bin          # 检查是否存在该目录文件夹
        vim ~/.bashrc                   # 修改环境变量，sudo vim修改root用户

        在文件最后一行添加：  export PATH="/usr/local/cuda/bin:$PATH"

        source ~/.bashrc                # 更新环境变量
        su - abc nvcc -V                # 再进行测试，发现可以读取了
        ```