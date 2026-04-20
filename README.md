# hust操作系统课设

**利用codex无痛完成头歌实验**

**请自行添加任务书，解压已有的基础实验包**

## 配置环境

1. **安装docker desktop**

   这里我安装的是orbstack

2. **拉取镜像（m芯片为例）**
   `docker pull docker.io/tjr9098/arm64_pke_mirrors:1.0`


   **拉取完检查一下**
   `docker images | grep pke`

3. **创建挂载本地仓库的容器**

   在**本地终端**执行

   ``````
   docker run -it \
     --name pke_mirror \
     --platform linux/arm64 \
     -v "/Users/breakfast/Desktop/项目/操作系统课设:/workspace" \
     -w /workspace/代码/lab1.2 \
     docker.io/tjr9098/arm64_pke_mirrors:1.0 \
     /bin/bash
   
   ``````

   - --name pke_mirror：容器名字叫 pke_mirror
   - --platform linux/arm64：明确使用 arm64
   - -v "...:/workspace"：把你本地仓库挂载到容器里的 /workspace(**注意修改**)
   - -w /workspace/代码/lab1.2：进入容器后默认工作目录就是 lab1.2（**注意修改**）
   - /bin/bash：启动一个交互 shell

4. **在容器内验证工具链**

   **进入容器**后，检查：

   ```
   pwd
   ls
   which riscv64-unknown-elf-gcc
   which spike
   which riscv64-unknown-elf-objdump
   ```

5. **编译运行**

   ```
   make clean
   make
   make run
   ```

****

## 使用codex

1. **安装codex**

   不过多赘述，这里用的是桌面端

2. **在项目目录下导入agents.md**

3. **写好prompt**
   **以lab4_challenge2为例，注意*加粗*的信息需要你自行根据每一关进行修改，同时更新*附件*和*预期输出内容***

   **当然你也可以在实验前汇总这些信息并写入agents.md，把头歌上的测试集附件下载到指定目录告诉codex。**

   

   ### Prompt：

   ***

   现在进行实验**lab4_challenge2**,严格遵守agents.md，着重阅读实验文档，理清需求完成实验目标优先，注意不要自作主张的改进一些与实验目标没有关系的代码，除非这些代码影响到实验目标的完成。 
   做好版本管理，按照要求每次对话完成后及时git更新。 每次改动代码部分实验文档必须按照要求及时更新。
   工具环境均已经配好，docker容器已经拉取到相关镜像，并与本地链接，你可以切换工作目录后直接make，make run。 
    这一关实验**不允许/允许**修改config.h。所有测试集文件均不允许修改！且不允许增删任何目录里的文件，如实在有必要，请告知我。 

   ***

   希望在测试集A(输入为**app_exec**)下，预期输出为：

   ```
   ------------------------------
   ls "/RAMDISK0":
   [name]               [inode_num]
   ------------------------------
   User exit with code:0.
   no more ready processes, system shutdown now.
   System is shutting down with exit code 0.
   ```

   ------------------------------

   在测试集B（输入为**app_exec2**）下，预期输出为： 

   ```
   ------------------------------
   read: /hostfile.txt
   file descriptor fd: 0
   read content: 
   This is an apple. 
   Apples are good for our health. 
   
   ------------------------------
   User exit with code:0.
   no more ready processes, system shutdown now.
   System is shutting down with exit code 0.  
   ```

   ***

   测试集文件已经**见附件**，他们都存放在user文件夹下。
   同时头歌上的user目录还比我们本地目录多了**两个只读的辅助文件app_ls.c与app_read.c**，也一并附上供你理解，注意这两个文件不可以修改，测试集文件也不可以修改。
     注意本地运行环境和头歌的测试集环境可能有不同，A、B测试集均属于头歌测试集。 
    注意写实验报告文档时最后要添加输入为**app_exec和app_exec**的输出截图。

***



## 总结

需要告诉智能体**每个实验对应的文件路径**、**实验指导书的位置**、**测试集内容和预期输出**、**允许修改哪些文件**。

尤其要注意如果你**使用git继承基础实验**之后，头歌上的挑战实验会比你继承的实验**多一些文件（主要在user文件夹下）**，且头歌上的挑战实验中有些文件**不允许修改**。

**这也是为何本地能出结果头歌没过关的原因。**
