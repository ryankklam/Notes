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