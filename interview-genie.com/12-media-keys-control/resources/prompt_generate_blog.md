【---
slug: how2use
title: 面试精灵使用手册
date: 2024-12-15T19:32:27.154Z
excerpt: 本文将为您介绍AI面试助手——面试精灵的基础功能，并为您在使用过程中遇到的常用问题进行解答。
coverImage: https://pic.interview-genie.com/00-interview-genie-how2use-main-sm-0528.jpg
tags:
  - Documentation
---

# 介绍
面试精灵是以顶级GPT为核的AI面试助手，从简历优化、在线面试回答、笔试助手、到面试记录与分析，提供全流程的面试辅助。助您拿到心仪的大厂Offer！

面试精灵的在线面试回答功能非常强大。支持简历和岗位描述文档上传，以期更了解你的经历和描述，生成更个性化、更贴切的回复。利用实时语音识别系统，声纹识别技术，结合长上下文大模型快速深入理解面试官意图。使用 RAG（检索增强生成） 技术进一步扩充强大GPT的知识，轻松应付各类面试问题。支持双栏模式，极速&精准我全都要。面试精灵--最懂你，最懂面试官，最懂知识的大模型AI面试助手。

# 快速引导
1. 设置：[面试/笔试前的准备-设置](https://interview-genie.com/blog/how2use/#%E9%9D%A2%E8%AF%95%E5%89%8D%E7%9A%84%E5%87%86%E5%A4%87-%E8%AE%BE%E7%BD%AE)
2. 面试助手：[面试操作](https://interview-genie.com/blog/how2use/#%E9%9D%A2%E8%AF%95%E7%95%8C%E9%9D%A2%E4%B8%80%E8%A7%88)
3. 笔试/测评：[笔试功能](https://interview-genie.com/blog/how2use/#%E7%AC%94%E8%AF%95%E5%8A%9F%E8%83%BD%E4%BB%8B%E7%BB%8D)

# 使用教程

## 注册与登录

新用户打开[面试精灵应用网站](https://interview-genie.com/)后，打开侧边栏，点击左下角登录按钮，打开登录页面。（您也可以点击右上角“设置”按钮，在弹出对话框中点击“登录”按钮，从而打开登录页面。）

![登录页面](https://pic.interview-genie.com/00-interview-genie-how2use-auth-sm.jpg)

未注册用户点击“注册”进入注册页面，完成注册（推荐使用不会被墙的邮箱，如QQ邮箱等）。注册后，您将收到激活邮件，激活后即可开始使用**面试精灵**。

已注册用户，输入用户名、密码后，点击“登录”，即可开始使用**面试精灵**的功能。

## 面试功能介绍
### 进入面试界面
登录账号后，点击左侧“面试助手”，即可进入面试界面，使用面试功能。

### 面试前的准备-设置
#### 设置语音输入模式
首先，您需要根据您的使用场景，参考下图选择语音输入模式。目前**面试精灵**支持以下语音输入模式：
![语音输入设置&声音指纹](https://pic.interview-genie.com/11_how_1.jpg)

##### “自动-多人聊天”模式

面试精灵在“自动-多人聊天”模式下，通过声音指纹自动分辨您和面试官的声音，并只对面试官的提问进行回答。在实战使用面试精灵辅助面试前，您需要录入自己的声音，以生成您专有的声音指纹。操作过程如上图所示：

1. 点击右上角“设置”按钮
2. 选择“音频”进行音频输入相关设置
3. 点击“声音指纹”部分的语音按钮，并根据指示朗读“我可以轻松搞定任何面试”，静音3秒后音频内容自动上传，生成并返回声音指纹。
4. 点击“更新声音指纹”完成个人声音指纹设置。现在我可以区别您和面试官啦^_^

“自动-多人聊天”模式允许您在电脑或移动设备上监听面试对话，并辅助您完成面试。该模式具有极高的隐蔽性，适用于任何面试软件和本机操作系统。

##### “自动-会议音频”模式
除了“自动-多人聊天”模式，我们还提供“自动-会议音频”语音输入模式，该模式具有更高的语音识别准确率，是当前默认语音输入模式。该模式下，用户需要提前选择语音输入的来源，如“浏览器标签页”或是“整个屏幕”，并勾选“同时分享系统/标签页中的音频”。然后，面试精灵会自动转录输入源中的音频作为面试官的声音来源。注意：Mac系统出于安全考虑，禁止分享系统音频，但仍可以分享标签页中的音频。所以Mac系统用户在使用非网页会议软件进行面试的时候，或是存在屏幕监控等情况下，建议选择上面介绍的“自动-多人聊天”模式。

![选择标签页或系统音频作为输入](https://pic.interview-genie.com/00-interview-genie-how2use-screen-audio_sm.jpg)

##### 其他模式
除了上面两种语音输入模式，您还可以使用“手动”、“自动-一对一”语音模式与**面试精灵**交流。您还可以直接通过文本输入框来使用**面试精灵**。

#### 设置“如何触发GPT回复”
在“设置”->“音频”->“如何触发GPT回复”中，您可以选择“手动触发”或“自动触发”来设置**面试精灵**何时进行AI辅助回答。
- 默认“手动触发”GPT回复，在这种模式下，您需要手动点击“文本输入框”上方的“AI快答”按钮，触发GPT回复，这种模式可以为您节省开销。
- 您也可以选择“如何触发GPT回复”为“自动触发”，这样每次面试官说完话，都会自动触发AI快答，该模式开销较高，但是让您免于手动操作。

当环境噪音大，或者音色差别不大的情况下容易出现说话人识别错误的问题，导致无法触发自动辅助回复。但是也没关系，您可以手动触发“AI快答”按钮（人工点击或媒体按键控制），大模型自动分析历史对话中的面试问题，无论说话人。  
##### 媒体按键控制触发GPT回复
另外，您还可以在面试页面的“快捷设置栏”中，设置开启“媒体按键控制”。该功能开启后，通过已连接设备的耳机的“播放”、“暂停”、“上一首”、“下一首”按键（实际按键点击方式由具体耳机型号决定，如有的耳机双击播放键实现“下一首”功能），来控制AI辅助回复时机。这样就能避免视频面试时候手动点击屏幕容易暴露的问题，提升面试精灵使用隐蔽性。搭配在非面试设备上使用“自动-多人聊天”对话模式，录入外放声音，媒体按键控制AI快答时机，面试精灵真正做到了绝对地安全隐蔽、支持所有面试平台和视频软件。  
具体按键使用说明如下：  
![媒体按键控制功能说明](https://pic.interview-genie.com/12-media-keys-control-details-table-xs.png)

耳机控制按键的具体控制功能如下：  
- **面试助手开启媒体按键控制后**
  - 当点击耳机“播放”或“暂停”按钮，则触发“AI快答”按钮，回复对话中大模型未回复的问题。若无未回复问题则回复上一次回复的问题。若当前为AI辅助回复中状态，则点击耳机“播放”或“暂停”按钮会触发“停止生成回复”按钮。
  - 点击耳机“下一首”，则会触发“发送”按钮，将输入框内容输出并进行“AI快答”。若当前为AI辅助回复中状态，则会先“停止生成回复”，然后触发“发送”按钮。
  - 点击“上一首”，则会触发最后一次AI回复的“重新生成”按钮。
- **笔试助手开启媒体按键控制后**
  - 当点击耳机“播放”或“暂停”按钮，则触发远程“截图”，同时“发送”默认Prompt请求大模型回复图中笔试题。若当前为AI辅助回复中状态，则点击耳机“播放”或“暂停”按钮会触发“停止生成回复”按钮。
  - 点击耳机“下一首”，则会触发远程“截图”，同时“发送”默认Prompt请求大模型回复图中笔试题。若当前为AI辅助回复中状态，则会先“停止生成回复”，然后触发“截图”和“发送”。
  - 点击“上一首”，则会触发最后一次AI回复的“重新生成”按钮。

目前由于各设备、各浏览器、各耳机类型的支持存在差异，我们不完全测试了如下组合是否支持使用“媒体按键控制”功能：  
![媒体按键控制功能支持情况](https://pic.interview-genie.com/12-media-keys-control-suppport-table-xs.png)

**符号说明：**  
- ✓ 完全支持  
- △ 不完全支持。面试助手部分情况下，部分耳机完全支持，可自行尝试  
- ⍻ 仅支持笔试助手使用  
- ✗ 不支持  
- ? 未查证/状态未知

**其他说明：**
- 有时候媒体按键会被其他软件捕获，可以关闭其他音频软件（如 Mac 电脑将“音乐”软件切换到主页，避免播放页捕获媒体按键），或是尝试切换浏览器类型。
- 如果您的设备或耳机使用媒体按键控制无反应，建议向朋友借下设备进行测试和面试。如果还是不行，建议使用其他回复触发方式。

> 强烈建议您花上十分钟，和朋友一起练习使用面试精灵实时面试功能，以免贻误战机。

#### 面试信息设置
打开“面试准备”对话框，即可进行面试信息设置，包括个人简历、目标公司、目标岗位等。有两种方式打开“面试准备”对话框，操作步骤如下：  
![AI联网搜索设置](https://pic.interview-genie.com/05-upgrade-interface-for-more-information-prepare-0407v1.png)

1. 登录账户：首先，确保您已登录面试精灵网站。
2. 打开“面试准备”对话框：
   - 在主界面点击“新建面试”
   - 或在面试界面点击输入框左下角的“面试信息设置”按钮

##### 选择大语言模型版本
我们提供了两种大语言模型版本，您可以根据需要选择。  

1. “面试准备”对话框中找到“大语言模型版本”选项。
2. 调整选项：
- “🔥专业强化版”
- “🚀极限精英版”：更强推理能力、更强理解能力

模型评测结果请点击链接查看：[「面试精灵」新一代AI引擎评测](https://interview-genie.com/blog/extreme-llm/)
定价信息请点击链接查看：[面试精灵-定价](https://interview-genie.com/blog/pricing/)

##### AI 联网搜索
开启“AI联网搜索”功能非常简单，只需按照以下步骤操作：

1. “面试准备”对话框中找到“联网搜索模式”选项。
2. 调整选项：
- 禁用：禁用此功能，不进行联网检索。
- 开启：启用此功能，AI将在回答问题时深度思考检索关键字并检索相关信息，然后使用检索结果优化回答效果。
- 自动：系统将根据问题的性质智能决定是否启用联网搜索。

**效果**

如果当前回复使用了“AI联网搜索”功能，则会在回复的状态栏实时显示检索关键字、检索进度、检索到的文章数量及列表。
回复文本下方会列出实际引用到的文章列表，并在回复内容中标注引用文章，方便您检验结果准确性。
![AI联网搜索效果图](https://pic.interview-genie.com/04-new-feature-AI-search-demo.jpg)

**功能亮点**

- AI 联网搜索：通过关键词分析自动检索实时信息，解决时事、技术动态等“时效性难题”。
- 幻觉率降低：结合权威信息源，减少错误回答风险。
- 信息可回溯：回复内容中标注引用文章，方便您检验结果准确性。

> 使用“AI联网搜索”功能会增加响应延迟，并增加token开销，请您根据实际需求选择。

##### 双栏模式
您可以在“面试准备”中开启或关闭“双栏模式”。  
开启双栏模式后，系统将并发地生成两栏结果，然后并排显示：“极速”栏响应迅速，便于快速提供思路、避免卡顿；“精准”栏结合更强的大模型和 RAG 技术提供更准确的答案。  

![双栏模式效果](https://pic.interview-genie.com/two-columns-CN-0528-sm.jpg)

“极速”栏和“精准”栏的主要区别：  
- **“极速”模式**：不利用简历、联网信息，仅利用部分上下文，使用“🔥专业强化版”大模型生成回复。回复速度极快，一般在1秒内给出答案首帧，方便您快速获得回答思路，避免卡壳。
- **“精准”模式**：系统将应用前面提到的设置（简历、联网搜索模式、大模型版本等）生成“精准”模式答案。优点是对于难题、时效性知识、冷门知识、逻辑推理题的准确率提高明显，可大大降低回复的幻觉率。该模式缺点是响应时间较长。

**双栏模式使用小贴士**：
- **极速栏定价**：“极速”栏开销极小（每题约0.1元），建议屏幕宽度允许的条件下尽量开启。具体定价来说，“极速”模式token数较少，token单价与“🔥专业强化版”大模型相同。
- **放大显示**：双栏模式下，双击任一栏结果，将放大该栏结果全屏显示。再次双击后即可重新变为两栏并排显示。
- **手机（小屏设备）上使用双栏模式**：推荐打开全屏模式、隐藏导航栏、设置字体大小为“超小”，以获得最大结果展示空间。

> 建议您实际使用中结合双栏输出结果进行使用以达到最佳辅助效果，精确栏推荐使用“🚀极限精英版”大模型、简历优化、联网搜索以确保获取更精准的结果。  
> 下面是一个典型的结构化回答的例子，请您参考：  
> - 第 0 秒：面试官提出问题；  
> - 第 1 秒：建议您一边重复面试官的问题，一边点击“AI 快答”按钮，触发回答，一般来说，重复问题会耗费 10s 左右，而回答会在 3s 内生成；  
> - 第 3 秒：（此时您依然在重复面试官的问题，您也可以针对问题的细节进行追问），此时“极速”模式回答已经生成，您可以开始默默阅览回答，并开始组织语言；  
> - 第 10 秒：（此时您已经阅览完毕，可以开始回答），此时您可以开始回答，回答的内容可以参考回答的内容，但不要完全照搬，否则会显得不自然；  
> - 第 30 秒：此时您根据“极速”模式的回答给出了一个初步的答案，此时“精确”模式回答应该已经准备完毕，您可以根据“精确”模式的回答组织语言，对您的回答进行补充。  
> 
> 多线程从来不是一件容易的事情，对于人类来说更是如此，但经过一段时间的练习，您会发现您的回答会变得更加流畅，更加自然。

### 面试界面一览
点击“面试助手”打开面试聊天框后，您将看到如下图所示的界面，您可以通过图中的标注来了解每个功能的作用。

![操作页面](https://pic.interview-genie.com/00-interview-genie-how2use-main-sm-0528.jpg)

前面提到的设置，部分可在上图界面顶部的“快捷设置栏”中进行快速地开启或关闭。

### 面试过程
在“自动-多人聊天”语音输入模式下，点击语音按钮，将持续录入、识别、分辨您和面试官的语音。在“自动-会议音频”语音输入模式下，系统将获取标签页或系统音频作为面试官语音输入。

我们将针对面试官的问题，结合您上传的文档（简历、职位描述、参考资料），当前聊天记录，使用顶级的大模型为您生成答案。

使用“手动触发”或“自动触发”（当前自动触发还待优化）来触发AI辅助回答。您也可以开启“媒体按键控制”，用耳机按键控制AI辅助时机。具体可以参考前面的**设置“如何触发GPT回复”**章节。

如果您对生成的结果不满意，可以在第一次生成完成后，点击生成结果下方的“再次生成”按钮，重新生成满意的结果。

### 面试后
点击“清除上下文”按钮，在弹出的对话框中，点击“备份并清空”，将保存当前对话历史到“文档”标签页，同时清除当前窗口，方便开始新的面试。您可以在“文档”标签页查看历史保存的面试记录，建议您为面试记录更改合理的名字。

当然您也可以选择点击“全部清空”按钮，抛弃对话历史，并重新开始新的面试。

## 笔试功能介绍
### 进入笔试界面
登录账号后，点击左侧“笔试助手”，即可进入笔试界面，使用笔试功能。

### 笔试前的准备
#### 笔试设置
笔试设置和笔试准备对话框设置方法参考前面的：[面试前的准备-设置](https://interview-genie.com/blog/how2use/#%E9%9D%A2%E8%AF%95%E5%89%8D%E7%9A%84%E5%87%86%E5%A4%87-%E8%AE%BE%E7%BD%AE)

笔试推荐开启“🚀极限精英版”大模型，获取最佳回复效果。

#### 笔试设备连接服务器
在您将要进行笔试的设备上，按如下图所示步骤操作，将该设备连接到服务器。
![笔试设备上连接服务器](https://pic.interview-genie.com/00-interview-genie-how2use-written-connect.jpg)

1. 打开“面试精灵”网站，登录后进入“笔试助手”页面。
2. 然后点击右下角的“连接”按钮。
3. 最后在弹出框内选择“分享”整个屏幕。

注意：在分享整个屏幕后，屏幕下方会弹出提示框“interview-genie.com正在共享您的屏幕”。为保证笔试助手使用的隐蔽性，请点击最右侧“隐藏”按钮。对于Mac电脑，即使隐藏提示框，在下方程序坞还会显示缩略图标，为保证绝对隐蔽性，您可以对Mac系统进行如下设置：“系统设置” >> “桌面与程序坞” >> “自动隐藏和显示程序坞”。

### 笔试中
####  另一台设备远程截图提问
以另一台（移动）设备作为“控制”设备，打开“面试精灵”登录同一账号后，进入“面试助手”页面，进行远程截图并发起提问，利用视觉大模型回答图片中的笔试问题。支持裁剪图片，只回答框定矩形框内的问题。具体操作步骤如下图所示。
![其他（移动）设备上进行远程截屏](https://pic.interview-genie.com/00-interview-genie-how2use-written-screenshot.jpg)

1. 在另一台“控制”设备上，点击“截图”按钮，触发已连接服务器的笔试设备上进行截屏，并发送到本设备上。
2. （可选）点击输入框中传入的截屏图片，在弹出界面中，选中图片中矩形区域后，点击“保存”按钮，将替换完整屏幕截屏为裁剪后的图片。
3. 点击发送按钮，识别图片中的问题，并回答。

您也可以开启“媒体按键控制”，然后耳机连接“控制”设备，使用耳机按键控制远程截图和AI辅助时机。具体可以参考前面的**设置“如何触发GPT回复”**章节。  

最终回答效果如下图所示：
![笔试助手回复结果](https://pic.interview-genie.com/00-interview-genie-how2use-written-result.jpg)

### 笔试后
在笔试设备上，再次点击“连接”按钮，断开连接。

和“面试助手”页面相同，您也可以选择保存笔试记录。

# 常见问题
## 1. 如何保障用户隐私？
我们承诺不记录用户的任何除账户基本信息之外的内容，您的隐私将得到最大程度的保护。个人上传文档、聊天记录仅个人账户登录可见。

## 2. 无法共享窗口音频怎么办？
不同类型设备安全限制不同，移动设备（手机/平板）仅支持录制外放声音，Mac增加支持录制浏览器音频，Windows在此基础上再增加支持录制全屏幕音频，不支持录制非浏览器软件音频。您需要根据您的使用场景和设备类型选择合适的对话模式和语音监听对象。  
手机/平板上使用还需要注意前面问题中的确保浏览器地址开头为 https:// 而不是 http://。  
如果排查后还是无法录音，建议您换一台设备试试。电脑推荐使用windows系统。浏览器推荐较新版chrome。

## 3. 手机/平板上怎么用？
移动设备（手机/平板）和电脑的操作基本一致，操作简单，无需下载app，网页打开即可使用。移动设备上使用有两个需要注意的地方：a. 只支持“自动-多人聊天”对话模式。b. 需要确保浏览器地址开头为 https:// 而不是 http:// ，即浏览器地址为：https://interview-genie.com

## 4. 支持ai面试/牛客网/微信视频/...么？支持金融/医疗/...行业面试么？
都支持的哦~面试精灵支持您在非面试设备（如另一台手机/平板）上进行面试辅助，共享屏幕也不怕，绝对的隐蔽安全，支持所有视频软件、面试平台。建议您在非面试设备上的设置-音频-对话模式中选择“自动-多人聊天”模式，该模式支持录入您的声音指纹。在实时面试的时候，自动识别说话人和面试官问题，然后为您生成满意答案。  
面试精灵强大的大模型能力搭配联网搜索能力，轻松一堆各行各业、各类面试问题，支持ai面试，用魔法打败魔法~

## 联系我们
欢迎您使用小红书扫码关注我们，实时获取更多面试精灵功能更新发布。
![面试精灵小红书二维码](https://pic.interview-genie.com/interview-genie-XiaoHongShu.jpg)

如果您有任何功能建议或遇到问题，我们邀请您点击下方链接后，微信扫码，加入面试精灵用户群，请不吝赐教。
更多联系方式请点击：[联系我们](https://interview-genie.com/blog/contact-us)

## bug 反馈
如果您在使用过程中遇到问题或bug，请即时反馈给[我们](mailto:interview-genie@qq.com)】

上面是面试精灵网站的使用说明。下面是其中AI联网搜索功能的PR稿：
【---
slug: new-feature-ai-search
title: 金三银四招聘季，“面试精灵”又发新功能——AI联网搜索
date: 2025-03-17T17:31:27.154Z
excerpt: 金三银四招聘季，正是收割 Offer 的好时候。基于大模型的AI面试助手--面试精灵又添新功能：AI联网搜索。通过网络检索最新的技术发展、时事分析、公司简介信息，提高时效性问题回复效果，降低大模型幻觉率，助您拿到心仪 Offer。赶紧注册体验吧！
coverImage: https://pic.interview-genie.com/04-new-feature-AI-search-demo.jpg
tags:
  - News
---

# 引言
春天来了，万物复苏，又到了～招聘～的季节～

又是一年一度的“金三银四”招聘季，相信很多小伙伴都在忙着准备面试吧。短短两个月的面试黄金期，可谓时间紧任务重。社招的小伙伴们可能还在被老板催着加班吧，哪来的时间复习算法题。校招的同学们大概无论怎么努力复习，都觉得知识点太多根本复习不过来。

别担心，面试精灵正是为解决这些问题而生。面试精灵是以顶级GPT为核的AI面试助手，从简历优化、笔试助手、在线面试回答、到面试记录与分析，提供全流程的面试辅助。助您拿到心仪的大厂Offer！

此前，用户反馈使用面试精灵时发现一个痛点：面对“2025年最火的大模型是哪一个？”这类时效性问题时，模型容易陷入“胡编乱造”的幻觉。为此，我们重磅推出 AI 联网搜索功能，让面试准备不仅有深度，更能紧跟前沿动态！

快来体验吧 >> [interview-genie.com](https://interview-genie.com)

原文地址：https://interview-genie.com/blog/new-feature-ai-search

关键字：Interview Genie, 面试精灵, AI面试助手, 简历助手, ChatGPT 面试, 大模型面试, 大型语言模型, 面试大师, 智能面试, AI笔试助手, AI联网搜索, 金三银四招聘季

# 介绍
AI 联网搜索使用 AI 分析出要完成当前问题需要搜索的关键字，并调用搜索引擎检索相关信息。然后以这些搜索结果作为补充信息，优化回答效果。

功能亮点：
- AI 联网搜索：通过关键词分析自动检索实时信息，解决时事、技术动态等“时效性难题”。
- 幻觉率降低：结合权威信息源，减少错误回答风险。

# 如何开启？
开启“AI联网搜索”功能非常简单，只需按照以下步骤操作：  
![AI联网搜索设置](https://pic.interview-genie.com/05-upgrade-interface-for-more-information-prepare-0407v1.png)

1. 登录账户：首先，确保您已登录面试精灵网站。
2. 打开“面试准备”对话框：在主界面点击“新建面试”或在面试界面点击输入框左下角的“面试信息设置”按钮，打开“面试准备”对话框。
3. 展开“高级面试设置”，找到“联网搜索模式”选项。
4. 调整选项：
- 禁用：禁用此功能，不进行联网检索。
- 开启：启用此功能，AI将在回答问题时深度思考检索关键字并检索相关信息，然后使用检索结果优化回答效果。
- 自动：系统将根据问题的性质智能决定是否启用联网搜索。

# 效果咋样？
如果当前回复使用了“AI联网搜索”功能，则会在回复的状态栏实时显示检索关键字、检索进度、检索到的文章数量及列表。
回复文本下方会列出实际引用到的文章列表，并在回复内容中标注引用文章，方便您检验结果准确性。

回答效果如下图所示：
![AI联网搜索效果图](https://pic.interview-genie.com/04-new-feature-AI-search-demo.jpg)

引入“AI联网搜索”功能后，面试精灵在处理以下类型的问题时表现出显著改善：

1. 最新科技进展
   面试官用该类问题考察应试者对前沿技术的跟踪。示例：“2025年初国内爆火的AI大模型是哪个？介绍他的技术特点”
   ![AI联网搜索效果对比图1](https://pic.interview-genie.com/04-new-feature-AI-search-compare1.jpg)
2. 热点时事分析
   示例：“你了解特朗普2025年上任后的关税政策么？对于中国的发展有什么影响？”
   ![AI联网搜索效果对比图2](https://pic.interview-genie.com/04-new-feature-AI-search-compare2.jpg)
3. 企业简介与发展近况
   该类问题主要用于考察应试者对于目标岗位目标公司的了解程度。“你了解我们支付宝公司的核心价值观么？我们公司最近发生了五分钟 bug 事件，这个事你怎么看？”
   ![AI联网搜索效果对比图3](https://pic.interview-genie.com/04-new-feature-AI-search-compare3.jpg)

通过实际测试，我们发现该功能不仅提高了回答的准确性，还大幅减少了大模型可能出现的“幻觉”现象，即生成与现实不符的信息。

更多使用技巧，请访问[面试精灵使用手册](https://interview-genie.com/blog/how2use)查看。

# 注意事项
使用“AI联网搜索”功能有以下几点需要留意：
- 耗时：由于涉及到网络搜索，使用“AI联网搜索”功能可能会使回答响应时间延迟。
- 开销：使用“AI联网搜索”功能可能会增加token消耗，每个问题回答的耗费会有所增加。
- 部分问题回答效果有回退：对于某些特定问题，尤其是那些需要深度专业知识的问题，联网搜索可能不会显著提升回答质量。
请根据实际需求评估，合理设置“AI联网搜索”功能的状态。


# 联系我们
欢迎您使用小红书扫码关注我们，实时获取更多面试精灵功能更新发布。
![面试精灵小红书二维码](https://pic.interview-genie.com/interview-genie-XiaoHongShu.jpg)

如果您有任何功能建议或遇到问题，我们邀请您点击下方链接后，微信扫码，加入面试精灵用户群，请不吝赐教。
更多联系方式请点击：[联系我们](https://interview-genie.com/blog/contact-us)

# 结语
面试精灵的目标是做懂你，懂面试官，懂知识的大模型AI面试助手。我们希望通过不断的技术创新和用户反馈，打造出能够切实帮助用户解决实际问题的强大工具。

本期更新的“AI联网搜索”能够帮助您解决更多复杂面试问题，快来体验吧！>> [interview-genie.com](https://interview-genie.com)

您的每一次反馈都是对我们最大的支持，感谢您的使用和支持！】

请参考【AI联网搜索PR稿】，结合结合上述【和】之间的面试精灵使用说明中关于最新功能“媒体按键控制”功能的说明，生成一篇介绍最新功能“媒体按键控制”功能的PR稿。注意SEO优化，降低营销感，输出完整笔记后，请指出具体做了哪些SEO优化和转化技巧。