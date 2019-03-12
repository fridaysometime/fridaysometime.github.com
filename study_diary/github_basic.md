# github_basic

## 基本创建仓库等

1. 创建仓库，安装Git bash

2. 打开git bash, 输入以下命令生成密钥用来验证身份

   ```bash
   ssh-keygen -C 'your@email.address' -t rsa
   ```

    连续三个回车之后会在windows当前用户目录下生成.ssh文件夹，和linux一样。（默认路径下：比如C盘user下）

3. 把文件夹下的id_rsa.pub文件内容全部复制

4. 打开github账户的setting，选择SSH and GPG keys

5. 选new ssh keys: 粘贴过去保存；

6. Git bash验证认证正确：

   ```bash
   ssh -T git@github.com
   ```

   正确结果会显示：

   ```bash
   Warning:Permanently added 'github.com,207.97.227.239' (RSA) to the list of known hosts.
   Hi Flowerowl! You've successfully authenticated, but GitHub does not provide shell access.
   ```

​	warning 不用理会。

7. clone新建的仓库到本地

   ```bash
   git clone XXX.git
   ```

8. 拷贝文件到本地该目录下，切换到git bash命令行，该目录的根目录下：

   ```bash
   git init
   git add '所有新增文件或文件夹'
   git commit -m '所有新增文件或文件夹'
   git remote add origin https://github.com/Flowerowl/stumansys.git(若报错already exists,要先remove，git remote rm origin)
   git push origin master(若报错failed to push som refs to,先pull再push，执行git pull origin master)
   ```

**git init初始化**

git init 命令只做一件事，就是在项目根目录下创建一个`.git`子目录，用来保存版本信息。

**git add**

git add --all/ git add .

对当前项目的所有变动改的文件保存并存在暂存区

**git commit**

暂存区保留本次变动的文件信息，等到修改的差不多，把信息写历史，相当于生成当前项目的一个快照；

项目的历史由不同时间点的快照构成；git可以将项目恢复到任意一个快照；

快照在 Git 里面有一个专门名词，叫做 commit，生成快照又称为完成一次提交。

git提供git commit命令，简化提交操作，保存进缓存区后，只要git commit一个命令，就同时提交目录结构和说明，生成快照；

git commit -m 'description'

**git checkout**

切换到某个快照

## 分支等

1. 查看分支

   ```bash
   git branch # 列出本地的分支
   git branch -r # 列出远端分支
   git branch -a # 列出所有分支
   git branch -v # 查看各个分支最后一个提交对象的信息
   git branch --merge # 查看已经合并到当前分支的分支
   git branch --no-merge # 查看未合并到当前分支的分支
   ```

​	 

2. 创建分支

   ```
   git brance feature-A # 创建一个名为feature-A的分支
   git checkout feature-A # 切换到feature-A分支
   git checkout -b feature-A # 创建并切换到feature-A分支
   git checkout -b feature-A dev # 基于dev新建feature分支
   ```

3. 删除分支

   ```
   git branch -d test # 删除test分支
   git branch -D test # 强制删除test分支
   ```

4. 合并分支

   ```
   git merge test # 把test分支合并到当前分支
   git merge --no-ff feature-A
   ```

## Pull Request （PR）

### 如果想参与别人的项目

1. 在github.com上fork到自己仓库

2. clone到本地

3. 建立一个branch

   ```
   git branch work
   git checkout work
   ```

4. 编程工作

5. push到自己的网站

   ```
   git add path/file_name.py
   git commit -m "填写你的说明"
   git push origin work
   ```

6. 在github上发送PR