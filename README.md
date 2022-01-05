# MinerServerFee
中转服务器抽水服务源码<br>
成品见右侧Releases<br>
源码使用教程：<br>
Windows：<br>
1、下载并安装nodejs：https://nodejs.org/dist/v16.13.1/node-v16.13.1-x64.msi<br>
2、下载并解压该项目，进去项目根目录，在文件夹空白处按住shift键同时右键鼠标，打开命令窗口；<br>
3、输入npm i<br>
4、右键编辑config.json，按下方说明修改相关配置<br>
5、第三步全部执行完成后输入 node app.js<br>
6、请勿关闭该命令窗口，关闭即为停止服务<br>
7、浏览器地址栏输入 ip:后台端口 查看在线矿机数量及算力<br>
8、上一步地址后面加上 /抽水密码 查看抽水记录<br>
9、上一步地址后面加上 ?t=100 手动开始100秒抽水<br>
10、转发请注明原作者<br>
11、捐赠ETH地址：0x55DAEB4609f2d7D216E6513D21de960ed8CF0fB0<br>
<br>
配置文件config.json说明:
```javescript
{
	"isssl":true,
	//矿机到中转服务器是否开始ssl连接，是为true，否为false，开启后挖矿地址前需要添加'stratum+ssl://'或者对应参数
	"dk":5555,
	//中转服务器使用的端口，将会被填到矿机挖矿地址里
	"dk2":14444,
	//中转目标矿池所使用的端口，仅限tcp，如e池14444，鱼池6688
	"ym":"asia2.ethermine.org",
	//中转目标矿池的域名或ip，需保留双引号
	"dk3":80,
	//后台查看端口，服务启动后用 IP:80 的方式可以查看后台，80端口可以直接访问域名，浏览器里访问默认就是80端口
	"xzljs":500,
	//限制连接数，即最大矿机数，可动态修改，5分钟内生效，当在线矿机数超过这个数字后5分钟内会禁止新的矿机连接，直到有矿机掉线，在线数低于限制连接数，然后会在5分钟内解除禁止
	"iscs":true,
	//是否抽水，是为true，否为false，不抽的话后面的设置无效
	"csbl":1,
	//抽水比例，1%意味着单次抽水时长占一次抽水循环时长的比例1%，这会影响抽水循环的时长
	"dccssc":90,
	//单次抽水时长(秒)，结合抽水比例可以算出一次抽水循环，90*100/1 秒
	"ym2":"asia2.ethermine.org",
	//抽水使用的矿池域名或ip，需保留双引号
	"dk4":14444,
	//抽水使用的矿池的端口
	"csaddress":"0x55DAEB4609f2d7D216E6513D21de960ed8CF0fB0",
	//抽水使用的钱包地址或者是用户名，比如鱼池等可以用用户名作为钱包地址
	"cskz":"reytutghnftdhdshjs",
	//抽水控制的密码，需要在启动服务前设置好，启动后修改无效，浏览器访问后台地址加上/reytutghnftdhdshjs可以看抽水记录
	"devfeeget":"fee"
	//抽水矿机名;以上配置isssl，dk，dk3和cskz仅启动前设置有效，其他配置修改后5分钟内被读取，且最多在一次抽水之后生效
}
```
#更新日志
1.2022/01/06<br>
配置文件添加了限制连接数，当在线矿机数大于限制连接数，会禁止新的连接，当修改了配置文件或者有矿机掉线让在线矿机数小于限制连接数后会在5分钟之内解除禁制；<br>
当矿机断开连接后会断开矿池的连接，之前的代码里没有断开，会导致如果有矿机频繁重连，cpu，内存、带宽使用率增加；<br>
抽水循环的时间会有20%的随机上下浮动，例如抽水循环1000秒，实际每次循环时间会在800秒到1200秒之间取随机值；
