//----------------------------人格对话AI数据文件-------------------------------------
------------------------------------对话说明-----------------------------------------
\1\s[12]唔？\w9\w9\s[10]\n我有做了什么吗？
\0\s[2]咦！\w9\w9\s[1]\n啊…\w9谢谢…
在上述语句中，
\1 指的是斗和来回答你的对话
\0 指的是橘花来回答你的对话

\w9 是等待时间
\s[10] 是调用第几个表情
\n 是换行
以下是表情的编码（不同的衣服可能不一样）：
0 正常
1 害羞(侧面)
2 惊讶
3 渴望
5 高兴
6 闭眼
7 生气
8 苦笑
9 尴尬
10 斗和(闭眼)
11 斗和(睁眼）
12 斗和(睁眼正视)
13 斗和(扭头无视)
20 思考
21 恍惚
22 P90
23 刀
25 唱歌
26 正面
27 电锯
28 礼物
29 幸福
30 侧面
32 手枪
33 委屈
34 军刀
35 难过
40 前屈
41 前屈(闭眼)
50 端茶
51 用餐

111 正常(人形）
也可以用<P90>代替\s[22]。
-----------------------------------添加说明------------------------------------
请按照格式添加，SESSION代表一个话题，Q代表问，A代表答，Q中有并列关键字用&分开。多个Q或A代表同义句。保存记事本为“任意文件名.ai”->所有文件->UTF-8。不能回答的对话关键字会自动保存在user.ai中，请将此文件反馈至右键斗和->推荐网址->项目地址
1.<think><set name="topic">帮忙</set></think>    //将话题变量topic设为"帮忙"
2.<topic name="帮忙"><srai>会&什么</srai></topic>    //话题变量topic等于"帮忙"时，执行<srai>会&什么</srai>
3.<srai>会&什么</srai>    //<srai>到</srai>的内容会被当作用户输入重新搜索数据库。
4.<A><that>要喝点什么吗</that><srai>来一杯红茶</srai></A>  //<that>到</that>
中的内容检查是否包含在橘花回答中，是的话提取后面的内容作为唯一输出，<that>可以和</topic>连用
<A><topic name="爱上你"><that>不是开玩笑的</that><惊讶>啊……<幸福>好的。。。</A> //当话题变量topic等于"爱上你"时，如果存在<that>，并且其内容匹配，提取</that>后面的内容作为唯一输出，如果不匹配，则放弃整句回答。
5.<Q>有&加油吗</Q>中的"&"表式同时匹配“有”和“加油”，无关其顺序。
6.<Q>*是*</Q>中*表式任意字符，只要在任意提问中包含"是"就算匹配，其匹配的*内容可以用<star/>或<star index="2"/>提取出来，<star/>表示第一个*代替的内容，<star index="n"/>表示第n个*代替的内容
当*出现在<that>中如<that>什么是*</that>，则可以用<thatstar/>提取出来
7.<if name="intimacy" greater="1000"></if>  //if 判断模式，“name=”后面是要判断的变量名，后面的greater是关键字，表示大于，即intimacy大于1000时，如果条件满足，则保留回答内容，否则放弃。此外还有关键字less,value,greatername,lessname,valuename,依次是小于、等于、大于、大于变量名的值，小于变量名的值、等于变量名的值。后三个关键字的使用如：
<if name="腹黑度" greatername="萌度"></if>
<if name="依赖度" lessname="幸福度"></if>
<if name="亲密度" valuename="依赖度"></if>
-----------------------------------橘花推理对话说明------------------------------------

方法1：“记住熊猫吃竹子”、“记住小黑是熊猫”
格式：”小黑吃什么“，答小黑是熊猫，所以吃竹子

方法2：“记住熊猫吃竹子”、“记住小黑吃竹子”
格式1：“熊猫吃什么”，答熊猫吃竹子
格式2：“什么吃竹子”，答熊猫吃竹子或小黑吃竹子
格式3：“小黑是什么”，答熊猫吃竹子，所以吃竹子的小黑是熊猫

方法3：“记住小张是人”，“记住人吃饭”
格式1：“小张吃什么”，答小张是人，所以吃饭
格式2：“小张吃饭吗”，答是的

方法4：“记住a是b的平方”、“b是c的平方”
格式1：“a是b的什么”，答a是b的平方
格式2：“a是c的什么”，合a是c的平方的平方

方法5：“记住A是B的爸爸”、“记住B是C的爸爸”、“记住C是D的爸爸”、“记住爸爸的爸爸是爷爷”
格式1：“A是B的什么”，答A是B的爸爸
格式2：“A是C的什么”，答A是C的爷爷
格式3：“A是D的什么”，答A是D的爸爸的爸爸的爸爸
格式4：“A是C的爷爷吗”，答是的，A是C的爷爷。
格式5：“A不是B的爸爸吗”，答不，A是B的爸爸
格式6：“A是B的爷爷吗” ，答A是B的爸爸

方法6：“记住小明是摩羯座”、“记住摩羯座是脚踏实地、意志坚定、为人谦逊、有幽默感的人”
格式1：“摩羯座是怎样的人” 答摩羯座是脚踏实地、意志坚定、为人谦逊、有幽默感的人
格式2：“小明是怎样的人” 答小明是摩羯座，所以是脚踏实地、意志坚定、为人谦逊、有幽默感的人

方法7：“记住小王是农民”，“记住农民种田”
格式1：“小王是做什么的”，答小王是农民
格式2：“小王干些什么” ，答小王是农民，所以种田
