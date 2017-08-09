# Detour规则简要说明

1. Detour基于[NEKit](https://github.com/zhuhaow/NEKit)，因此你可以看到一些NEKit规则的影子。同样基于NEKit的产品如[Wingy](https://github.com/hellowingy/wingy-announcement)，规则都类似。
2. 多条规则冲突时，先加入的规则会生效。
3. 只有选择了(界面上打了勾)的规则才会生效。
4. 相同的代理不用重复建...

## 每个用户都想到的一件事
>"Detour配置起来好麻烦"  "这玩意怎么用啊看不懂"

>"为啥要手动建这么多规则啊！"

>"XXX配置要简单多了！Detour作者怎么想的！"

其实Detour和其他客户端的处理方式稍有不同，其他客户端是基于代理，而Detour是基于规则，这也是为什么Detour配置这么多规则。到这我知道您可能还是一脸懵逼。好，接下来我开始辩解。

Detour的好处在于，当你有多个节点时，你可以控制每个节点去处理哪个请求，比如打游戏的用节点A，tumblr的用节点B，twitter的用节点C。（我会在最后做个简单示例）自由度高，配置起来自然就麻烦了。
>"我就一个节点！我用不到！配置真麻烦，老子不用了！"

。。。我错了，大爷。等以后有时间会更新一个傻~~逼~~瓜版的功能。(

## 举几个栗子🌰
### Shadowsocks全局代理（即所有流量都途经VPN）
1. 在Detour配置页面,点击添加新代理，类型选择Shadowsocks，其他信息也依次填入并保存。（再次说明，账号密码你们自己去搞...搞不到的就简单的用用广告屏蔽功能也挺好的。）
2. 在Detour配置页面，点击添加新规则，类型选择All，代理选择你刚刚新建的代理，标题随便写。
3. 在Detour配置页面，点击一下新添加的规则，确保前面是打了勾的，然后就可以去状态页面开启啦。

### Shadowsocks智能代理（即访问国外走代理，访问国内直连）
1. 在Detour配置页面,点击添加新代理，类型选择Direct，标题随便写（最好与当前的信息相关，省的弄混，比如这里可以写直连），保存。
2. 在Detour配置页面,点击添加新代理，类型选择Shadowsocks，其他信息也依次填入并保存。（如果你上一步做过了就不必重新加了）
3. 在Detour配置页面，点击添加新规则，类型选择Country，国家代码写CN，是否匹配选择是，标题写中国🇨🇳，代理选择刚刚新建的直连，保存。
4. 在Detour配置页面，点击添加新规则，类型选择All，代理选择你刚刚新建的Shadowsocks代理，标题随便写。（先建立的规则会先匹配，所以这一步一定要在第三步之后做）
5. 在Detour配置页面，选择刚刚新添加的两条规则，确保前面是打了勾的，然后就可以去状态页面开启啦。

### 广告屏蔽（类似这种规则一定要先建立，这样会先匹配到，才能起到屏蔽广告的效果）
1. 在Detour配置页面,点击添加新代理，类型选择Reject，标题随便写，保存。
2. 在Detour配置页面，点击添加新规则，类型选择List，IP列表写agn\\.aty\\.sohu\\.com，代理选择刚刚新建的Reject。（这条规则是针对搜狐视频的，这里只是举个例子，多条IP用回车隔开）

### 内网直连
1. 在Detour配置页面,点击添加新代理，类型选择Direct，标题随便写（最好与当前的信息相关，省的弄混，比如这里可以写直连），保存。
2. 在Detour配置页面，点击添加新规则，类型选择IP List，IP列表范围写127.0.0.0/8，代理选择刚刚新建的Direct。

### 说好的简单示例
1. 添加四个代理,类型分别是Direct、Reject、Shadowsocks(tumblr节点),Shadowsocks(Twitter节点)。
2. 添加规则，`List`类型，代理选择`Direct`的，名字可以叫做`苹果和本地直连`,内容如下：
```
apple.com
icloud.com
itunes.com
crashlytics.com
mzstatic.com
localhost
.cn
```
3. 添加规则，`IP List`类型，代理选择`Direct`,名字可以叫做`内网IP直连`，内容如下：
```
127.0.0.0/8
192.168.0.0/16
10.0.0.0/8
224.0.0.0/8
169.254.0.0/16
```
4. 添加规则,`List`类型，代理选择`Reject`,名字可以叫做`屏蔽地址`，内容暂时没找，自己去找，可以把你所知道的广告地址都写进来，正则也好，关键字也好。多条用回车隔开。
5. 添加规则，`Country`类型，代理选择`Direct`,代码`CN`,匹配`是`，名字`大陆直连`。
6. 添加规则，`DNSFail`类型，代理选择`Tumblr节点`,名字`DNS无法解析`
7. 添加规则，`List`类型，代理选择`Twitter节点`,名字`推特专属`，内容填个`twitter`。
8. 添加规则，`All`类型，代理选择`Tumblr节点`,名字`汤和其他`。
9. 勾选所有规则，大功告成，一个比较通用的例子.

## 最后
如果你有任何问题，iamldj#163.com~~反正我也不会~~
  
