# WebGAL

### 一次编写，处处运行，无需网页开发基础，3分钟即可学会所有的语法，只要你有灵感，就可以立刻开始开始创作你自己的Galgame！

## 在线演示

https://wg.msfasr.com

国内访问这个链接可能会更快： https://webgal.loveshan.pw/ （感谢大佬提供的CDN）

## 如果你是想要开发属于自己的 Galgame 的开发者，请下载发行版：

https://github.com/MakinoharaShoko/WebGAL/releases/

如果下载速度过慢，请尝试通过蓝奏云网盘下载(版本不一定是最新的，建议在 GitHub Release 下载）： https://wwm.lanzouw.com/iWGiJzehoni


> 想要参与引擎开发的开发者请先阅读 [此项目的参与指南](/DEV_NOTE.md)

## 如何在本地运行WebGAL？

## 新手可以尝试使用 WebGAL Terre 编辑器技术预览版，这是一个图形化的 Galgame 脚本编辑器。

[图形化编辑器](https://github.com/MakinoharaShoko/WebGAL_Terre)

[图形化编辑器的前端代码仓库](https://github.com/MakinoharaShoko/WebGAL_Origine)

**注意：图形化编辑器的功能有限，如果你需要更高级的演出，请学习本文档的脚本。**

#### Windows用户可以使用以下方式快速打开调试界面:

现在，你可以直接运行WebGAL-win.exe即可开始调试你的视觉小说。如果遇到杀毒软件拦截或防火墙拦截等情况，请放行以允许该程序运行。

#### 其他用户：

WebGAL理论上可以在任何浏览器上运行，但是由于浏览器的**限制跨域访问**机制，本地 JavaScript 脚本可能无法在浏览器上运行，因此，你需要在本地建立一个http服务器。你可以选择任何你喜爱的的http服务器，并通过本地http服务器访问index.html来开始游戏。如果你没有本地http服务器，你可以使用Node.js简单地搭建一个。

我在**WebGAL发行版**的根目录放置了一个app.js作为 Node.js 服务器脚本，在你安装了 Node.js 后，只需要通过以下命令：

```shell
npm install express
npm install open
node app.js
```

即可开始调试你的游戏。

### 如何将我的Galgame部署到互联网上，并使他人能够访问？

首先，请知悉，可以部署到互联网的引擎应该是**发行版**，而不是源代码。

复制/WebGAL 下的文件(不是文件夹，是/WebGAL 文件夹下的文件)到你想要部署的云服务器的指定目录下，或是部署到GitHub Pages。

如果你使用源代码进行调试，你可以通过 npm run build 或 yarn run build 来创建一个静态网页（在/build 文件夹），然后将这个文件夹内的内容部署到 GitHub Pages 或你的云服务器上。

*如果你需要避免程序被破解，可解除UserInteract.js中373~378行的注释，从而使别人无法打开F12（使用npm/yarn build时无须这么做）*

# 游戏制作快速上手教程：

现在，你应该已经运行起来了一个调试服务器，接下来让我来教你如何编写你自己的剧本

你应该能够发现，在解压后的文件夹下，有一个 WebGAL 文件夹，在 WebGAL 文件夹下，有一个 game 文件夹，那就是你的游戏资源应该存放的地方。

你的所有游戏剧本、图片、立绘都应该在放解压后目录的 WebGAL/game 文件夹下，目录对应的资源说明如下：

| 文件夹     | 存放的资源                   |
| ---------- | ---------------------------- |
| background | 用于存放背景图片、标题页背景 |
| figure     | 用于存放人物立绘             |
| scene      | 用于存放用户剧本             |
| bgm        | 用于存放背景音乐             |
| vocal      | 用于存放配音文件             |
| video      | 用于存放视频                 |

## 定制你的游戏信息

在/game 文件夹下，有一个文件config.txt，你可以在这个文件中填写你游戏的相关信息：

```
Game_name:WebGAL;//你的游戏名称
Game_key:0f33fdGr;//一串识别码，你应该尽可能随机地输入一串不容易与别人重复的字符，长度最好在6-10字符之间，否则可能会引发bug
Title_img:Title2.png;//标题的图片名称，图片放在/background 文件夹
Title_bgm:夏影.mp3;//标题的背景音乐，音乐文件应该放在/bgm文件夹
Loading_img:Loading_img.jpg//游戏进入时Logo，放在/background 文件夹
```

## 用户剧本的编写语法：

首先，程序会从**初始脚本**`start.txt`开始运行，在后续的脚本编写中，我会告诉你如何跳转章节或设置分支选项。

**编写剧本的方式非常简单，且与自然语言几乎无异。**

### 首先，让我们来学习编写基本的人物对话：

首先，使用记事本或VS Code 、sublime 等文本编辑器，打开游戏资源目录下 scene 文件夹中的 start.txt，然后你就可以开始编写你的第一条对话了。

编写人物对话的方法非常简单，你只需要输入：

**注意，每条对话的冒号、分号应当为英文字符！**

```
人物:对话;
```

示例：

```
雪之下雪乃:请用茶;
由比滨:啊，谢谢;
小町:谢谢雪乃姐！;
一色:谢谢学姐。;
```

在每条对话/剧本后，使用分号作为结束。（如果不写分号有时候也行，但是作者还是建议加上分号以防止bug）。

#### 连续对话

如果你的多条对话没有改变人物名称，你可以使用连续对话，而可以省略人物名称，再在你需要的时候使用：

```
雪之下雪乃:你到得真早;
对不起，等很久了吗？;//此时，对话的人物名称仍然是“雪之下雪乃”。
比企谷八幡:刚到而已;
```

### 黑屏文字演示

在许多游戏中，会以黑屏显示一些文字，用来引入主题或表现人物的心理活动。你可以使用 intro 命令来演出独白：

```
intro:回忆不需要适合的剧本，,反正一说出口，,都成了戏言。;
```

独白的分拆以英文逗号(,)来分割，也就是说，每一个英文逗号代表一个换行。在实际演出中，上面的文字会变成：

```
回忆不需要适合的剧本，
反正一说出口，
都成了戏言。
```

具体的情况还请在游戏中自行试验。

### 改变背景/人物立绘：

要让 WebGAL 能够读取背景图片和人物立绘，你的背景图片应该被放在background文件夹内，而立绘图片则应该放在figure文件夹中。

接下来，你可以通过以下简单的语句来改变当前显示的背景图片和人物立绘：

```
changeBG:testBG03.jpg;//改变背景
changeP:testFigure02.png;//改变人物立绘
changeBG:none;//关闭背景
changeP:none;//关闭人物立绘
```

你有可能会发现，在你改变背景图片或人物立绘后，你需要再点击一下鼠标才能显示下一条对话，如果你希望在改变背景图片/立绘后立即执行下一条语句的内容，请使用：

```
changeBG_next:testBG03.jpg;
changeP_next:testFigure02.png;//改变人物立绘
一色:谢谢学姐！;
```

如果你这样做，那么在背景图片/立绘替换后，程序会立刻执行下一条语句。

### 放置小头像：

很多游戏可以在文本框的左下角放置小头像，以下是在本引擎中使用的语法：

```
miniAvatar:minipic_test.png;//在左下角显示minipic_test.png
miniAvatar:none;//关闭这个小头像
```



### 将立绘放在不同的位置

现在，你可以在页面的三个不同位置放置不同的立绘，只需要在放置立绘的语句处加上你要放置的位置就可以了，示例如下：

```
changeP_left:testFigure03.png;
changeP:testFigure04.png;
changeP_right:testFigure03.png;
```

以上三行分别对应着左、中、右三个不同的位置。三个不同位置的立绘是相互独立的，所以如果你需要清除立绘，必须分别独立清除：

```
changeP_left:none;
changeP:none;
changeP_right:none;
```

如果你想要在立绘改变后立刻执行下一条语句，操作方法与之前一样，即在命令后加上 `_next` :

```
changeP_left_next:testFigure03.png;
changeP_next:testFigure04.png;
changeP_right_next:testFigure03.png;
```

注意命令的书写顺序，如果你这样写（先写next后写位置），那么将是无效的：

```
changeP_next_left:testFigure03.png;
changeP_next_right:testFigure03.png;
```

### 跳转场景与分支选择：

在 Galgame 中，跳转章节、场景与分支选择是不可或缺的，因此，本游戏模组也支持场景跳转与分支选择。

你可以将你的剧本拆分成多个 txt 文档，并使用一个简单的语句来切换当前运行的剧本。

假如你现在写了两个章节的剧本，分别是 Chapter-1.txt 与 Chapter-2.txt ，在Chapter-1.txt 运行结束后，你希望跳转到 Chapter-2.txt 对应的场景，请使用以下语句：

#### 场景跳转：

语句：

```
changeScene:Chapter-2.txt;
```

示例：

```
(Chapter-1.txt)
......
......
changeScene:Chapter-2.txt;
接下来执行的就是Chapter-2.txt的内容了。
......
......
(Chapter-2.txt)
```

通过执行这条命令，你将切换游戏场景，并使接下来的剧情发展按照新的场景剧本运行。新的剧本会在下一次鼠标点击后运行。

#### 分支选择：

如果你的剧本存在分支选项，你希望通过选择不同的选项进入不同的章节，请使用以下语句：

```
choose:{叫住她:Chapter-2.txt,回家:Chapter-3.txt};
```

你只需要将选项的文本与选择选项后要进入的剧本名称一一对应起来，就可以实现分支选择的功能了。

### 引入背景音乐（BGM）

引入背景音乐的方法极其简单，你只需要将背景音乐放置在 /bgm 目录下，然后便可以简单地在需要的时候令其播放：

```
bgm:夏影.mp3;
```

### 播放一小段视频

```
playVideo:OP.mp4//视频应该放在/game/video/ 文件夹内
```

### 在显示对话时同时播放语音

众所周知，Galgame 最吸引人的地方往往在于其有优秀的配音。在此版本中，你可以为对话引入配音了，将你的配音放入vocal文件夹，然后在对话的前面，人物名称的后面加入 `vocal-语音文件名,`即可引入，语法示例如下：

```
比企谷八幡:vocal-V3.ogg,刚到而已;
```

在连续对话时，语音的引入方式也是一样的：

```
雪之下雪乃:vocal-V1.ogg,你到得真早;
vocal-V2.ogg,对不起，等很久了吗？;
```

### 使用动画效果

#### 为背景设置动画

使用语句 `setBgAni:动画名,时间(多少秒);`

背景动画设置之后会在每次替换背景时生效，除非再次使用`setBgAni`改变。

**示例：**

```
setBgAni:bg_softIn,5s;//渐入背景，执行5秒
```

目前，预制的动画只有两个：渐入和缩放渐入，使用的动画预设名分别为：

| 动画效果 | 动画名    |
| -------- | --------- |
| 渐入     | bg_softIn |
| 缩放渐入 | bg_down   |

#### 为人物设置动画

使用语句`setFigAni:位置,动画名,时间（多少秒）;`

```
setFigAni:right,rightIn,1s;//对右侧立绘设置动画rightIn，执行1秒
```

人物动画不像背景动画。每次设置动画时，这个动画都会立刻执行，且只执行一遍（因为你可能会设置一些例如摇晃之类的效果，但是不想让这个动画一直在切换人物时生效）

所以，你每次切换人物立绘，或是想要执行动画时，都要使用`setFigAni`:

```
changeP_left_next:testFigure03.png;
setFigAni:left,leftIn,1s;
//这个动画只对这一次changeP生效
changeP_left_next:testFigure04.png;
setFigAni:left,rightIn,1s;
//现在你改变了左侧立绘，如果你需要一个动画，你需要再重新设置
```

同时，在你没有改变立绘的时候，你也可以在某句对话前加上`setFigAni`，这样在播放这句对话的时候，动画会同时执行。

```
setFigAni:right,shake,0.5s;
右侧人物:现在我正在摇晃。//动画与这句对话同时执行
```

预制动画：

| 动画效果     | 动画名   |
| ------------ | -------- |
| 摇晃         | shake    |
| 从下向上进入 | upIn     |
| 从左向右进入 | leftIn   |
| 从右向左进入 | rightIn  |
| 渐显         | centerIn |
| 前后移动     | moveBaF  |

### 自定义动画

动画文件在`/StaticCSS/animation.css`，你可以学习CSS动画来自己写你想要的动画效果，然后添加到这个CSS里，在游戏脚本里用这个动画。

如：

```
@keyframes leftIn {
    0%{
        opacity: 0;
        transform: scale(1,1) translate(-5%,0);
    }

    100%{
        opacity: 1;
        transform: scale(1,1) translate(0,0);
    }
}
```

然后，你就可以使用

```
setFigAni:left,leftIn,1s;
```

调用这个动画。

## 进阶教程：

### 在同一个场景（TXT文件）内实现语句跳转、分支跳转

如果你想要创建一个分支，但是却觉得为此新建一个TXT文件太麻烦，你可以尝试使用以下方式在同一文件内实现创建分支和跳转语句。

**注意：如果你的分支很长，我不建议你使用这种方式，因为一个TXT的行数不适宜太长，否则可能会导致加载慢、响应迟钝等性能问题。**

#### 首先，你必须理解如何使用label：

```
......
jump_label:label_1;
//以下这些行会被忽略:
......
......
......
//然后，你需要创建label:
label:label_1;
然后，程序会在这里继续执行。;
......
......
```

简而言之， jump_label 类似于 goto 语句，能够立刻让你的剧本跳到场景（TXT文件）中的任意一个位置，而这个位置需要你用label创建。

如果把jump_label 比作任意门，那么这个任意门的终点就是 label 所在的位置。

#### 有了上面的基础，你就可以通过 choose_label 的方式来实现用分支来跳转到 label 所在的位置了：

```
WebGAL:让我们来测试分支跳转到label！;
choose_label:{测试1:label_1,测试2:label_2};
label:label_1;
现在应该是1号分支;
jump_label:end;
label:label_2;
现在应该是2号分支;
jump_label:end;
label:end;
现在是统一的结束;
```

注意，在每个分支的结尾，你应该用 jump_label 来跳转到你希望的位置。由于程序是线性执行的，所以如果你没有在分支的结束跳转，那么程序会继续往下运行，比如说：

```
WebGAL:让我们来测试分支跳转到label！;
choose_label:{测试1:label_1,测试2:label_2};
label:label_1;
现在应该是1号分支;
label:label_2;
现在应该是2号分支;
现在是统一的结束;
```

在这个剧本中，如果你选择了分支2，那么一切看起来好像没有问题。但是如果你选择了分支1，你会惊讶地发现，在分支1执行完后，竟然分支2又执行了一遍。那是因为程序按顺序继续执行下一行了，而你没有指定在分支结束后跳到哪里。

### 使用变量

**注意：这是一个测试功能，可能会发生未知异常**

**注意：在你弄清楚如何使用label，如何在label内部跳转场景之前，请不要轻易使用变量系统，这可能会令你感到迷惑！**

#### 语句介绍：

```
setVar:a=3,b=2;//a的值是3，b的值是2
setVar:a=a+1;//a的值+1
setVar:a=b+3;//a的值是b的值+3
setVar:a=1+a;//错误：不支持这种写法，+的前面应该是一个变量。
showVar:all;//该语句没有参数，直接输入 showVar:all; 即可在文本框里打印出所有的变量及其值。
if(a>=3):label1;//当a>=3时，跳转到label1
if(c=3):label2;//当c=3时，跳转到label2
if(a=c):label2;//错误：不支持这种写法
label:label1;
......
......
jump_label:end;
label:label2;
......
......
jump_label:end;
label:end;
......
......

//备注：
//以下是旧的写法，在现在的版本中仍然生效，并且与if语句的执行效果相同，但是不建议使用。
//保留这种写法是为了能够向下兼容旧的脚本，但是如果你正在写新的脚本，你可以直接用上面的新脚本。
jump_varReach:a:3,label1;//当a>=3时，跳转到label1
jump_varBelow:a:3,label2;//当a<3时，跳转到label2
varSet:a:1,b:1;//声明两个变量，a的值为1，b的值为1
varUp:a:2,b:3;//a的值提升2，b的值提升3
varDrop:a:1,b:3;//a的值降低1，b的值降低3
```

#### 如果我希望用if跳转到其他场景（也就是其他txt文件），我该怎么做？

**示例：**

```
setVar:a=0;//设置一个变量a（现在是0）
setVar:a=a+1;;//现在a=1
if(a=1):label1;//a=1时跳到label1
label:label1;//以下是label1的执行内容
changeScene:Ch2.txt;//在label1执行的语句内跳到Ch2.txt
......现在执行的是Ch2.txt的脚本了.......
......Ch2.txt......
```


## Stargazers over time

[![Stargazers over time](https://starchart.cc/MakinoharaShoko/WebGAL.svg)](https://starchart.cc/MakinoharaShoko/WebGAL)
