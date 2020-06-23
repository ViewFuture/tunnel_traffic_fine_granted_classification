# 隧道行为精细化分类调研
Matti 和MirKo 在2011年提出两阶段识别SSH隧道上应用类别的方法[1],第一阶段先识别出某条连接是不是SSH连接，第二阶段检测SSH隧道上面的应用类别。他们使用的是统计特征。【1】

Maurizio和Alice等人在2014年提出使用SVM和GMM方法检测SSH隧道上应用类型的方法【2】。他们使用的特征是每条SSH流的前N个包的带方向的包长序列。他们研究的行为类别分HTTP,POP3,POP3S,EMULE,MSN,HTTPS,BT。两种分类方法的识别准确率都可到达71.5%以上。

2018年来自北京邮电大学的LiuYong和Yijie 提出使用卷积神经网络识别SSH隧道上应用类别的方法。【3】他们研究的应用类别分Nmap,Baidu网盘,网易云音乐,网易词典和QQ五类，在验证集上他们的方法可以达到95.8%的准确率。他们的方法是将每一个数据包的payload转化为一张灰度图，然后使用CNN分类。

孟郊等人使用5类机器学习方法来识别SSH隧道上面的应用类别，他们使用的机器学习方法包括：C4.5决策树，SVM，Bayes网络，K-means以及EM算法。他们使用TCP握手完成后连续8个包的包长、包间隔时间以及包方向作为分类特征，分类的类别有HTTP over SSH，FTP over SSH,SCP & SFTP三分类，K-means的分类准确率可达到94.66%以上。【4】

李旭航于2019年提出使用XGBoost梯度提升树对SSH隧道应用进行分类的方法，分类类别包含HTTP,FTP,SMTP,SCP,Login共五种常见应用，使用的特征还是加密流量的统计特征，实验的识别准确率和召回率都在90%以上，其中对于HTTP协议的召回率达到了95.81%.【5】同时他在这篇硕士论文中对SSH隧道上流量识别的国内外现状做了总结。

2008年Dust提出使用【6】，他们研究了SSH隧道上POP3,SMTP,CHAT和P2P四类常见的应用。使用的特征是包长序列和包到达时间间隔序列，使用的机器学习方法是高斯混合模型，识别的准确率可以达到82.45%以上。

2014年管其玲在其硕士论文里面使用KNN作为分类器，使用流的包长序列，包达到时间间隔序列以及反向包比重作为特征对SSH上的HTTP和Other类别进行分类，HTTP over SSH的识别准确率可达到90%以上，但是该论文的实验样本及其少，缺乏代表性。【7】
	
2017年和留勇在其硕士论文中，提出使用神经网络对SSH隧道应用协议进行识别的方法，他的分类类别包括SSH隧道上的LT,RT,SCP,SFTP,X11,SHELL,TELNET,FTP,HTTP,DNS和P2P共11类，他使用的特征是数据包包长和到达时间间隔的统计特征。这11类应用的识别正确率都可达到98.7%以上，误报率在0.3%以下。【8】

和留勇还尝试识别SFTP上面传输的文件的类型，类型包括图片、音频、可执行文件、文本，使用CNN网络做分类器，在测试集可以达到92.9%的准确率。

2012年谭小兵提出使用高斯混合模型识别SSH隧道上面的HTTP,SMTP,POP3,FTP四类应用，他使用带方向的包长序列作为流量特征，模型的准确率可以达到87.57%。【9】

2018年Sam,Steven等人对VPN隧道、Tor隧道上面的四类应用HTTP,Skype,Youtube,Bittorrent 使用朴素贝叶斯、逻辑回归以及随机森林分类器进行分类，他们对包长、包到达时间间隔序列以及busrt特征的分类效果进行了对比。实验结果发现，在VPN隧道上，随机森林+包长+包到达时间间隔序列分类效果最好，可达到96.77%的正确率。【10】

还有一批学者把精力集中在加密隧道上web页面的精细化分类上。他们的主要任务就是：已知SSH隧道、VPN隧道或Tor隧道上是Web浏览的流量，推断出具体访问的是什么web页面。

2006年，Liberatore提出基于Jaccard相似度的KNN模型识别SSH隧道上面的web页面的方法。【11】他做的是1000分类，使用的特征是包方向和包长序列。Top10的实验结果可以达到90%的准确率。

2009年Herrmann提出借鉴文本挖掘领域使用多项式朴素贝叶斯模型识别OpenSSH,OpenVPN,CiscoVPN,Stunnel和Tor隧道上web网页的方法，他们是775分类，他们使用的主要特征是数据包大小的频率向量。在SSH和VPN隧道上，他们的方法可以取得94.94%以上的准确率。【14】

2010年，Liming Lu在Liberatore【11】的工作基础上提出利用数据包的顺序信息来增强加密隧道上网页的识别准确率的方法。【13】他们考察了该方法在VPN隧道，SSH隧道上的实际效果，该方法相比Liberatore的工作可以提高10个百分点，而且对于混淆的流量可以使得分类效果得到更大的提升。他们还使用编辑距离作为KNN的相似度度量。

2014年YanShi提出使用贝叶斯网络+Burst特征+Haar特征识别VPN隧道上更新频繁的web页面的方法，他们动态网页选择了11类，同时他们还选择了11个静态网页作为对比。他们的实验方法以96.7%的准确率识别动态页面，97.8%的准确率识别静态页面。【12】
	

2015年Xiaodan Gu等人认为之前加密隧道上的web网站的识别没有考虑到用户在相对较短的时间内同时打开多个web页面的情况，而现实环境中用户在使用浏览器过程中短时间内相继打开多个tab的情况是比较常见的。作者使用朴素贝叶斯模型作为分类器，对alexa top 50进行分类。作者使用的特征包括TCP连接数，inbound和outbound的字节数，以及一些特殊的特征。【16】当假设用户只短期内相继打开2个页面，而且打开第一个页面后隔2s再打开第二个页面，那么他们的方法可以以75.9%的准确率识别第一个页面，以40.5%准确率识别第二个页面。

2017年 Tekachew和Hyoung 在Psiphon建立的VPN隧道上开展网站指纹攻击。【17】他们采用了基于包长的统计特征，并使用线性判别模型、SVM和KNN模型作为分类器。他们首先训练用于识别Psiphon和非Psiphon流量的分类器，这三个分类器都可以达到89.4%的准确率。之后他们又使用knn模型对Psiphon上的Alexa top 20个站点进行分类，发现分类的准确率只有33.1%。

2018年，Zhongliu Zhou提出基于轮廓隐马尔科夫模型识别加密隧道上的网站（website）的方法。与之前的网页（webpage）识别相比，加密隧道上的website识别是指只要确认用户是否访问过某个web网站的任意一个页面。Zhongliu认为在建立web网站指纹的时候，应该考虑同一个web网站的多个webpage以及这些webpage之间的超链接跳转关系，这是首例在web网站指纹中考虑超链接跳转关系的工作。Zhong同时考察了他的方法在SSH隧道和Shadowsocks隧道上，对网站和网页的识别效果。与K-Fingerprint相比，在Shadowsocks隧道上，Zhong的方法可以取得80%左右的website识别准确率,K-Fingerprint只有70%的准确率.【15】

2011年，Ding Yao-jun在ICCS上发表了使用C4.5决策树识别HTTP隧道的方法，他使用20维基于包长、包到达时间间隔的统计特征，分类类别包括HTTP,SMTP over HTTP,P2P over HTTP以及灰鸽子流量，实验环境下在测试集上可以达到95.3%以上的准确率。【18】

2019年，来自西电Lin Huaqing等人提出使用规则和机器学习方法混合的检测DNS隧道、HTTP隧道以及HTTPS隧道。他们会提取IP数据包的包长、包到达时间间隔，并提取相应的统计特征，他们也会提取DNS、HTTP隧道里面的特定字段作为特征。隧道里面的载荷协议类型包括SSH,SFTP,聊天协议以及远程桌面协议。他们还对比了不同的分类方法的分类效果，这些分类方法包括SVM,C4.5,随机森林，GBDT和XGboost。 随机森林在这三种隧道上都能达到99.99%的F1-score.【19】

# 参考文献
【1】Two-phased method for identifying SSH encrypted application flows
【2】Identifying the traffic of SSH-encrypted applications
【3】Identification of SSH Applications Based on Convolutional Neural Network
【4】Study on SSH application classification based on machine learning.
【5】基于XGBoost的SSH流量识别研究
【6】Tunnel Hunter Detecting Application-Layer Tunnels with Statistical Fingerprinting
【7】基于行为特征的SSH流分类系统研究与实现
【8】基于深度学习的SSH隧道下应用的精细化识别研究和实现
【9】SSH隧道流量检测与识别技术研究
【10】Fingerprinting encrypted network traffic types using machine learning
【11】Inferring the Source of Encrypted HTTP Connections
【12】Website Fingerprinting using Traffic Analysis of Dynamic Webpages
【13】WebsiteFingerprintingAndIdenti
【14】Website Fingerprinting attacking popular privacy enhancing technologies with MNB
【15】Website Fingerprinting attack on anonymity networks based on profile hidden markov model
【16】A novel website fingerprinting attack against multi-tab browsing behavior
【17】Website fingerprinting attack on Psiphon and Its Forensic Analysis
【18】A method for Http-Tunnel Detection based on statistical features of traffic
【19】Detection of Application-Layer Tunnels with Rules and Machine Learning

