## 在 Mac 上安装 lightGBM 的步骤
### 在 Mac 上安装 lightGBM 会出现好几个坑，本人几乎均已踩过，所以总结下该方案，按照步骤来，应该就可以了
- 首先放上官方链接  https://lightgbm.readthedocs.io/en/latest/Installation-Guide.html#macos。


### 1. 首先确保 Homebrew 已经安装并可以正常工作。
- 这也是第一个坑，如果 homebrew 不能正常工作，后续就没法进行，在 bash里输入命令 ```brew install cmake```, 如果可以正常安装 brew 可以正常工作，否则就需要解决第一个问题。卸载 Homebrew, 再重装。为保证卸载干净我们执行两步。
  - 第一步，执行卸载命令   
  ```/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"``` 
  - 第二步，检查 usr/local/ 目录下是否有文件夹 Homebrew, 如果有则直接删除
  - 第三步，执行安装命令  
  ```/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" ```
  - 执行命令 ```brew update``` 将 homebrew 更新到最新
### 2. 参照官网，安装 cmake, gcc
- 执行以下命令
    - ```brew install cmake```
    - ```brew install gcc```  
    (如果报错，请使用命令 ```brew reinstall gcc```)
### 3. 将路径加入到系统环境
- 执行命令 (注意 vim 编辑器的使用，如果不会的话可以参照第一篇里面将 conda 路径加入到 bash 的方法)
  - ```vim ~/.bash_profile```
  - ```export PATH="/usr/local/Cellar/gcc/8.3.0/bin:$PATH"```
### 4. 安装 lightGBM
- 执行以下命令：
  ```
  git clone --recursive https://github.com/Microsoft/LightGBM ; cd LightGBM
  export CXX=g++-8 CC=gcc-8
  mkdir build ; cd build
  ```
### 5. cmake 编译 lightGBM
- 执行命令 
  ```
  cmake ..
  make -j4
  ``` 
    - **如果**上面两行命令报错，则尝试执行 
      
      ```
      sudo cmake -DCMAKE_CXX_COMPILER=g++-8 -DCMAKE_C_COMPILER=gcc-8 ..
      sudo make -j4
      ```
此时尝试 import lightgbm 如果可以，表示已经成功了，如果还不行，请继续下面的步骤(大概率是不需要的)：

执行 ```cd ../python-package```  
然后 ```sudo python setup.py install --precompile```  
然后 ```pip install lightgbm```
 
