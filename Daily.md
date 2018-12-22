# Daily standup

##2018.01.10
>每一分都不能浪费啊，今日在聊maven跟Jenkins setup的时候感觉大家都懂得很多呢，2018.01.11 先重新setup maven，整份guideline吧.
***
##2018.01.11
>Maven打通了，注意先加cert然后master pwd然后普通pwd，注意setting.xml在golbal config，user config不要override。 太多野比jessie搞，需要balance一下， 2018.01.12 check下auto testing个jenkins setup.
***

##2018.01.12-19
>之前hk出差都是开会多，工作基本没怎么做。不过这周Jenkins setup通了，现在可以自动trigger build while push requst to branch. 下周可以看看G3deploy 或者 setup个AOC或VNM的UAT env in gitHUB
***

##2018.01.20
>hk出差电话卡都不见了，补办了但手续超级麻烦，去交行补身份证又branch没开门。
***

##2018.01.20
>hk出差电话卡都不见了，补办了但手续超级麻烦，去交行补身份证又branch没开门。
***

##2018.03.14
>香港回来喉咙痛周身无力，今日休息一天，同老豆沟通了一下，发现问题还是很大，老豆喜欢将小问题放大，而且觉得是我学坏了。但这可能有联系，即生活习惯改变。太过于放松导致慵懒，看来是需要严于律己。
***
=======
##2018.01.22
>今日本来开会讲sprint又没搞，GitHUB的UAT setup没搞，jenkins也没搞，就sent了个mail给Jinu回了hcm然后拿到了contact，催了下albert，然后capture了两个cirr39的testacse，今日进展真是差！
***

##2018.01.29
>今日同kyo chris午餐，问左下近况，risk真系黑。晚上回来单车革新路兜了一圈，什么精品店都没有了，礼物没买成。
***

##2018.02.22
>过年放per左好多日，沉迷辐射。今日了解了一点serverless的concept，感觉未必是很成熟，需要继续观察。
***

##2018.02.26
>就是plan了下一个sprint的task。Eric跟Mark抽到了大利是。Luis问了zookeeper如何handle几个node，答不上来。看了下chatbot的source，有简单的NLP。明天继续看看source
***

##2018.03.27
>本来想迅速教jay ccode好个notifyDate的unittest，竟然发现mockito mock不了static method。转而引入powerMockito，用法不难，小米讲左两次个File load module，其实就是一个checkfile availablity的野,可以定好接口然后尝试code个简单sample给他（springboot ？）。 明天搞掂Jay坛野。
***

##2018.04.05
>油猴真是好工具，竟然有一个老司机脚本，可以自动改网页样式，不需要翻页，自动getlinkfrom search engine,post to 115
感觉稍加改动就可以自动返回smv的结果，值得一试。
***

##2018.04.07
>SpringBoot用上手包括embed H2用起来真是很方便，今日也有看点Actora（资源endpoint）跟Spring Boot Admin（dashboard，非spring官方）
配个简单入收json然后output db的操作，用jackson竟然失败，bean类field mark了private，而且没getter、setter
Jackson deserialize:
a public field
non-public field with getter or setter
明天搞好个api sample然后upload hithub，sent个mail出去给小米
***

## 2018.11.11
>荒废很久，突然想起，又重新记记吧
今天主要是上gcp online课程
***

## 2018.11.17
>Atom Markdown Preview ： ctrl-shift-m.
***

## 2018.12.22
>代码参数里的 payload 是什么意思 ？payload 字面意思 “有效载荷，有效负荷，有效载重”。
对于程序员来说，有效载重究竟是个什么玩意儿，又是一个新的问题.
要解释什么是有效载重，用货运行业打个比方：
比如有一位客户需要支付一笔费用委托货车司机运送一车石油，石油本身的重量、车子的
重量、司机的重量等等，这些都属于载重(load)。但是对于该客户来说，他关心的只有石
油的重量，所以石油的重量是有效载重(payload，也就是付费的重量)。

JMS规范目前支持两种消息模型：点对点（point to point， queue）和发布/订阅（publish/subscribe，topic）。

1.1、点对点：Queue，不可重复消费
消息生产者生产消息发送到queue中，然后消息消费者从queue中取出并且消费消息。
消息被消费以后，queue中不再有存储，所以消息消费者不可能消费到已经被消费的消息。Queue支持存在多个消费者，但是对一个消息而言，只会有一个消费者可以消费。

1.2、发布/订阅：Topic，可以重复消费
消息生产者（发布）将消息发布到topic中，同时有多个消息消费者（订阅）消费该消息。和点对点方式不同，发布到topic的消息会被所有订阅者消费。
***
