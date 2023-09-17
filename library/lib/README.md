- 静态库制作
  - `gcc -c xxx.c` : 得到.o文件
  - `ar rcs libxxx.a xxx.o` : 得到对应静态库文件
  - 将静态库文件和对应头文件放到指定位置
  - `gcc main.c -o app -I ./include -l calc -L ./lib` : 对main文件编译

- 动态库制作
  - `gcc -c -fpic xxx.c` : 生成和位置无关的代码
  - `gcc -shared xxx.o -o libxxx.so` : 生成动态库文件
  - `export LD_LIBARY_PATH=$export LD_LIBARY_PATH:/path/to/your/dir` : 导入环境变量
  - `gcc main.c -o app -I ./include -l calc -L ./lib`使用动态库编译
  - `ldd app` :查找可执行文件app依赖对应路径

- 解决动态库加载失败：
	- 导入环境变量： `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/path/to/your/so` 终端关掉后重新打开失效 
	- 用户级环境变量：
		- `vim .bashrc` 
		- 然后导入环境变量`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/path/to/your/so` 
		- 退出后重新执行.bashrc : `. .bashrc` 
	- 系统级：`sudo vim etc/profile` 后面同理
	- 配制`/etc/ld.so.cache` 
		- `sudo vim /etc/ld.so.conf` 然后将动态库的路径粘贴到该文件里，最后`sudo ldconfig` 
    