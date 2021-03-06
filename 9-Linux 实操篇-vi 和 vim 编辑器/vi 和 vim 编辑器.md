## vi 和 vim 编辑器

### 一、vi 和 vim 的基本介绍

Linux 系统会内置 vi 文本编辑器

Vim 具有程序编辑的能力，可以看做是 Vi 的增强版本，可以主动的以字体颜色辨别语法的正确性，方便程序设计。代码补完、编译及错误跳转等方便编程的功能特别丰富，在程序员中被广泛使用



### 二、vi 和 vim 常用的三种模式

#### 2.1 正常模式

以 vim 打开一个档案就直接进入一般模式了(这是默认的模式)。在这个模式中， 你可以使用『上下左右』按键来
移动光标，你可以使用『删除字符』或『删除整行』来处理档案内容， 也可以使用『复制、粘贴』来处理文件数据。

#### 2.2 插入模式

按下 i, I, o, O, a, A, r, R 等任何一个字母之后才会进入编辑模式, 一般来说按 i 即可

#### 2.3 命令行模式

输入 esc 再输入：，在这个模式当中， 可以提供相关指令，完成读取、存盘、替换、离开 vim 、显示行号等操作



### 三、vi 和 vim 基本使用

```bash
# vim 打开 Hello.java 文件。如果不存在，会自动创建，并用 vim 打开
vim Hello.java
```



### 四、vi 和 vim 三种模式的相互切换

![1650763642874](E:\code\linux\9-Linux 实操篇-vi 和 vim 编辑器\vi 和 vim 编辑器.assets\1650763642874.png)



### 五、vi 和 vim 快捷键

```bash
## 常用快捷键

# yy			拷贝当前行
# 5yy			拷贝当前行向下的 5 行

# p				粘贴

# dd			删除当前行
# 5dd			删除当前行向下的 5 行

# /关键字	  	  在文件中查找某个单词，输入 n 继续查找下一个

# set nu		设置文件的行号
# set nonu		取消文件的行号

# G				跳转到文档的最末行
# gg			跳转到文档的最首行
# 20 shift+g	跳转到文档的第 20 行

# u				撤销
```



![img](E:\code\linux\9-Linux 实操篇-vi 和 vim 编辑器\vi 和 vim 编辑器.assets\vim_cn.gif)



#### 5.1 一般模式可用的快捷键说明，光标移动、复制粘贴、搜寻取代等

| 移动光标             | 说明                 |
| -------------------- | -------------------- |
| h 或 向左箭头键（⬅） | 光标向左移动一个字符 |
| j 或 向下箭头键（⬇） | 光标向下移动一个字符 |
| k 或 向上箭头键（⬆） | 光标向上移动一个字符 |
| l 或 向右箭头键（➡） | 光标向右移动一个字符 |

如果想要进行多次移动，只需要先输入想要进行的次数（数字）后，按下相应动作即可，例如 30j 就是向下移动 30 行



|              |                                                              |
| ------------ | ------------------------------------------------------------ |
| [ctrl] + [f] | 屏幕向下移动一页，相当于 [Page Down]                         |
| [ctrl] + [b] | 屏幕向上移动一页，相当于 [Page Up]                           |
| [ctrl] + [d] | 屏幕向下移动半页                                             |
| [ctrl] + [u] | 屏幕向上移动半页                                             |
|              |                                                              |
| +            | 光标移动到下一行的非空格符位置                               |
| -            | 光标移动到上一行的非空格位置                                 |
|              |                                                              |
| n <space>    | 按下数字后再按空格键，光标会向右移动移动这一行的 n 个字符，相当于 nl |
|              |                                                              |
| 0 或 [Home]  | 移动到这一行的最前面字符处                                   |
| $ 或 [End]   | 移动到这一行的最后面字符处                                   |
|              |                                                              |
| H            | 光标移动到这个屏幕的最上方那一行的第一个字符                 |
| M            | 光标移动到这个屏幕的中央那一行的第一个字符                   |
| L            | 光标移动到这个屏幕的最下方那一行的第一个字符                 |
|              |                                                              |
| G            | 移动到文档的最后一行                                         |
| nG           | 移动到文档的第 n 行                                          |
| gg           | 移动到文档的第一行，相当于 1G                                |
|              |                                                              |



| 搜寻与取代            | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| /word                 | 向光标之下寻找一个名为 word 的字符串                         |
| ?word                 | 向光标之上寻找一个名为 word 的字符串                         |
| n                     | 重复前一个搜寻的动作。<br />如果前一个搜寻动作是 /word，则会继续向下寻找；<br />如果是 ?word ，则会继续向上寻找 |
| N                     | 与 n 相反<br />如果前一个搜寻动作是 /word，则会向上寻找<br />如果是 ？word，则会向下寻找 |
|                       |                                                              |
| :n1,n2s/word1/word2/g | 在 n1 与 n2 行之间寻找 word1 字符串，并将该字符串替换为 word2 |
| :1,$s/word1/word2/g   | 从第一行到最后一行寻找 word1 字符串，并将该字符串替换为 word2 |
| :1,$s/word1/word2/gc  | 从第一行到最后一行寻找 word 字符串，并将该字符串替换为 word2<br />且在取代前显示提示字符给用户确认（confirm）是否需要取代 |
|                       |                                                              |



| 删除、复制与粘贴 | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| x,X              | 在一行字当中，x 为向后删除一个字符（相当于[del]）<br />X 为向前删除一个字符（相当于 [backspace] 退格键） |
| nx               | 连续向后删除 n 个字符（如果不足 n 个字符，则删除到行末）     |
| nX               | 连续向前删除 n 个字符（如果不足 n 个字符，则删除到行首）     |
|                  |                                                              |
| dd               | 删除游标所在的那一行                                         |
| ndd              | 删除光标所在行的向下 n 行                                    |
| d1G              | 删除第一行到光标所在行的所有数据                             |
| dG               | 删除光标所在行到最后一行的所有数据                           |
| d$               | 删除光标所在处到行尾的所有数据                               |
| d0               | 删除行首到光标所在处的所有数据                               |
|                  |                                                              |
| yy               | 复制光标所在的那一行                                         |
| nyy              | 复制光标所在行的向下 n 行                                    |
| y1G              | 复制第一行到光标所在行的所有数据                             |
| yG               | 复制光标所在行到最后一行的所有数据                           |
| y$               | 复制光标所在处到行尾的所有数据                               |
| y0               | 复制行首到光标所在处的所有数据                               |
|                  |                                                              |
| p,P              | p 为在光标所在行与下一行之间粘贴复制的数据<br />P 为在光标所在行与上一行之间粘贴复制的数据 |
|                  |                                                              |
| J                | 将光标所在行与下一行的数据结合成同一行                       |
| c                | 重复删除多个数据，例如向下删除 10 行，10cj(不包括当前行，且切换到编辑模式) |
| u                | 复原前一个动作                                               |
| [ctrl]+r         | 重做上一个动作                                               |
|                  |                                                              |





#### 5.2 一般模式切换到编辑模式的可用的快捷键说明



| 进入插入或取代的编辑模式 | 说明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| i,I                      | 进入插入模式 [Insert mode]<br />i 为从目前光标所在处插入<br />I 为从目前光标所在行的第一个非空格字符处开始插入 |
| a,A                      | 进入插入模式 [Insert mode]<br />a 为从目前光标所在处的下一个字符处开始插入<br />A 为从目前光标所在行的最后一个字符处开始插入 |
| o,O                      | 进入插入模式 [Insert mode]<br />o 为从目前光标所在行的下一行插入新的一行<br />O 为从目前光标所在行的上一行插入新的一行 |
| r,R                      | 进入取代模式 [Replace mode]<br />r 只会取代光标所在的那一个字符一次<br />R 会一直取代光标所在的字符，直到按下 [Esc] 为止 |
| [Esc]                    | 退出编辑模式，回到一般模式                                   |



#### 5.3 一般模式切换到命令模式的可用的快捷键说明

| 存储、离开等指令    | 说明                                                         |
| ------------------- | ------------------------------------------------------------ |
| :w                  | 将编辑的数据写入硬盘档案中                                   |
| :w!                 | 如果文件属性为 [只读] 时，强制写入文件。不过，是否写入成功取决于用户对文件的权限 |
| :q                  | 离开 vi                                                      |
| :q!                 | 若层修改过文件，又不想存储，使用 !q 为强制离开不存储档案     |
| :wq                 | 存储后离开，如果 wq! 则为强制存储后离开                      |
| ZZ                  | 若文件没有修改，则不存储离开；若文件修改过，则存储后离开     |
| :w [filename]       | 将编辑的数据存储成另一个文件（类似于另存新档）               |
| :r [filename]       | 在编辑的文件中，读入另一个文件的数据，也就是将 [filename] 这个文件的内容加到光标所在行后面一行 |
| :n1,n2 w [filename] | 将 n1 到 n2 行的内容存储成 filename 这个文件                 |
| :! command          | 暂时离开 vi 到命令模式下执行 command 的显示结果<br />例如 :! ls /home 即可在 vi 当中查看 /home 的文档信息 |

| vim 环境的变更 | 说明         |
| -------------- | :----------- |
| :set nu        | 显示行号     |
| :set nonu      | 取消显示行号 |







