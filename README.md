
###网卡相关###

	创建网卡
		Ifconfig eth0 90.19.3.255 netmask 255.255.252.0
	配置网卡信息
		Vi  /etc/sysconfig/network-scripts/ifcfg-eth0
![Alt](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrEOi2ejd9xddqyOl6iBx8OPa3QB2Ll2avNlwNIQJyforxtRiPW96phokjH1OiigqnX6Ea3Ffwp7qBmJ6qSuMvq04!/b&bo=KgIdAQAAAAABFwQ!&rf=viewer_4)

###Linux下网卡重启命令###

	service network restart

###ping###

	查询本机正在使用网卡信息，进行设置ip

###Windows怎么打开注册表编辑器###

	CMD regedit

###进入数据库###

	Sqlplus “/as sysdba” 

###更换yum源###

	更换yum源，将原有源删除或备份到别的目录下：
	#cd /etc/yum.repos.d/
    #wget  http://mirrors.163.com/.help/CentOS6-Base-163.repo
	#vi CentOS6-Base-163.repo
	编辑文件，把文件里面的$releasever全部替换为版本号：6（注意，不是6.5！）最后保存！
		：%s/$releasever/6/g
	清除原有缓存，重建缓存： 
	#yum clean all 
	#yum makecache
	更新系统： 
	#yum update
	首先想到的是不是系统安装的时候没有装libc，于是执行
	# rpm -qa | grep libc
	可以看到是安装libc的，并且如果没有这个动态库的话，很多非系统命令将不能使用。
	接着想到的是查询系统中这个libc.so.6文件到底在哪
	[root@localhost ~]# find / -name libc.so.6
	建立强链接有问题，再次执行安装包，还是会出现同样的错误，于是换成软链接
	sudo ln -s /lib64/libc.so.6 /lib/libc.so.6

###VM安装Linux系统 无法正常安装###

	1、镜像文件与VM虚拟机需要安装文件不匹配；
	2、CPU问题 CPU未虚拟化 使用BIOS修改CPU设置
		选择“intel(R) Virtualization Technology” 这一项，默认为“Disabled”,禁用的，选择“Enabled”启用

###虚拟机链接远程工具###

	1、网络适配器选择链桥接；
	2、Ifconfig ethx ipaddr netmask x.x.x.x
		ethx中的x代表第几块以太网卡，默认第一块为0；ipaddr代表ip地址；x.x.x.x为子网掩码。
	3、配置网卡信息
		vi  /etc/sysconfig/network-scripts/ifcfg-eth0

###关闭防火墙的方法为：###

	1、永久性生效
		开启：chkconfig iptables on
		关闭：chkconfig iptables off
	2、即时生效，重启后失效
		yum install iptables-services
		开启：service iptables start
		关闭：service iptables stop
	--查询防火墙状态
		service iptables status

###linux下出现ping:unknown host www.baidu.com问题时的解决办法###

	1、最低级的错误没有关闭防火墙
	2、检查当前环境配置的IP信息 ifconfig
	3、检查网络配置是否正确 cat /etc/sysconfig/network-scripts/ifcfg-eth0
	4、ping一下设置的网关是否能够ping通,如果网关无法连通，则需要修改 /etc/sysconfig/network-scripts/ifcfg-eth0文件下的网关地址
	5、检查DNS服务器是否正确，使用命令 cat  resolv.conf
	6、ping配置的DNS服务解析地址，看是否能够ping通，如果无法连通，则需要修改，但必须
	7、保证是正常的能使用的DNS地址
	8、只有上述配置都无误后，就可以连通外网资源，再进行测试，是否能ping通外网资源

###Ext.js 数据 模型###

	modal的基类是Ext.data.Model.It表示应用程序中的一个实体。 它将存储数据绑定到视图

###Ext.js 数据存储###

	**静态存储**:...
	**动态存储**:可以使用代理获取动态数据。 我们可以让代理可以从Ajax，Rest和Json获取数据。

###Ext.js getSelectionModel获取选择的行可以进行如下操作###

	var model = grid.getSelectionModel();  
	model.selectAll();//选择所有行  model.selectFirstRow();//选择第一行  
	model.selectLastRow([flag]);//选择最后一行,flag为正的话保持当前已经选中的行数,不填则默认false  
	model.selectNext();//选择下一行  model.selectPrevious();//选择上一行  
	model.selectRange(tartRow,ndRow, [Boolean keepExisting] );//选择范围间的行  
	model.selectRow(row);//选择某一行  model.selectRows(rows);//选择指定一些行,传递数组如[1,3,5],则分别选择1,3,5行  
	model.clearSelections();//清空所有选择  model.deselectRange( startRow, endRow );//取消从startrow到endrow的记录的选择状态  
	model.deselectRow(row);//取消指定行的记录grid.getSelected().id //得到选中的行的标识

###LinkedHashMap 与 HashMap区别###

	LinkedHashMap 是HashMap的一个子类，保存了记录的插入顺序，在用Iterator遍历LinkedHashMap时，
	先得到的记录肯定是先插入的.也可以在构造时用带参数，按照应用次数排序。在遍历的时候会比HashMap慢，
	不过有种情况例外，当HashMap容量很大，实际数据较少时，遍历起来可能会比 LinkedHashMap慢，因为
	LinkedHashMap的遍历速度只和实际数据有关，和容量无关，而HashMap的遍历速度和他的容量有关。

###Oracle 输出、输入数据乱码问题###

	修改pl/sql developer 的编码格式：
	在windows中创 建一个名为“NLS_LANG”的系统环境变量，设置其值为“SIMPLIFIED CHINESE_CHINA.ZHS16GBK”，
	然后重新启动 pl/sql developer，这样检索出来的中文内容就不会是乱码了。如果想转换为UTF8字符集，
	可以赋予“NLS_LANG”为 “AMERICAN_AMERICA.UTF8”，然后重新启动 pl/sql developer。其它字符集设置同上。

###PLSQL无选框###

	1、缺少instantclient_11_2文件，获取文件放置到Oracle/product/ 文件夹下
	2、同时创建tnsnames.oraOR文件 product\11.2.0\client_1\network\admin
	3、无登录PLSQL 首选项设置 Oracle主目录名 即：instantclient_11_2文件位置
	4、设置OCI库 即instantclient_11_2/oci.dll 文件位置
	5、设置环境变量 TNS_ADMIN为tnsnames.ora所在目录

###Win10怎么设置窗口护眼色###

	regedit进入注册表
	HKEY_CURRENT_USER\Control Panel\Desktop\Colors：
	修改window默认值 204 238 208  
	\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Themes\DefaultColors\Standard       
 	修改window默认值 CCEED0

###Java中的Map遍历###

	遍历inMap 获取到每一个映射关系
	返回此映射中包含的映射关系的 Set 视图。返回值 嵌套类Map.Entry（映射项）

        for (Map.Entry<String, String> entry : inMap.entrySet())
        {
            ....
        }

###18.非关系型数据库和关系型数据库区别，优势比较？###

	关系型数据库和非关系型数据库在使用场景上差别比较大，所以并不存在孰强孰弱，只有结合自身的业务特点才能发挥出这两类数据库的优势，下面说说这两类数据库的一些特点：
	首先一般非关系型数据库是基于CAP模型，而传统的关系型数据库是基于ACID模型的

	1. 数据存储结构：
	首先关系型数据库一般都有固定的表结构，并且需要通过DDL语句来修改表结构，不是很容易进行扩展，而非关系型数据库的存储机制就有很多了，比如基于文档的，K-V键值对的，
	还有基于图的等，对于数据的格式十分灵活没有固定的表结构，方便扩展，因此如果业务的数据结构并不是固定的或者经常变动比较大的，那么非关系型数据库是个好的选择
	
	2. 可扩展性
	传统的关系型数据库给人一种横向扩展难，不好对数据进行分片等，而一些非关系型数据库则原生就支持数据的水平扩展(比如mongodb的sharding机制)，
	并且这可能也是很多NoSQL的一大卖点，其实象Mysql这种关系型数据库的水平扩展也并不是难，即使NoSQL水平扩展容易但对于向跨分片进行joins这种场景都没有什么太好的
	解决办法，不管是关系型还是非关系型数据库，解决水平扩展或者跨分片Joins这种场景，在应用层和数据库层中间加一层中间件来做数据处理也许是个好的办法
	
	3. 数据一致性
	非关系型数据库一般强调的是数据最终一致性，而不没有像ACID一样强调数据的强一致性，从非关系型数据库中读到的有可能还是处于一个中间态的数据，因此如果你的业务对于
	数据的一致性要求很高，那么非关系型数据库并不一个很好的选择，非关系型数据库可能更多的偏向于OLAP场景，而关系型数据库更多偏向于OLTP场景

###Windows  python3.7 pip安装###

	Python安装路径下 下载
	curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py python get-pip.py
	运行 get-pip.py

###Scrapy 数据爬取 重复不准确等问题###

	项目settings.py文件中，配置问题
	ITEM_PIPELINES = {
	    'scrapytest.MyPipelines.MyPipeline': 1,
	    'scrapytest.ImgPipelines.ImgPipeline': 100,
	}
	**item pipeline管道详细分析、过滤、存储优先级问题**

###配置Maven本地仓库###

	1、在D:\Program Files\Apache\目录下新建maven-repository文件夹，该目录用作maven的本地库。
	2、打开D:\Program Files\Apache\maven\conf\settings.xml文件，查找下面这行代码：
		<localRepository>/path/to/local/repo</localRepository>
	**localRepository节点默认是被注释掉的，需要把它移到注释之外，然后将localRepository节点的值改为我们自己创建的目录**

###Maven镜像仓库替换为阿里云镜像仓库###

	在本地 maven 的 setting配置文件中加上阿里云镜像地址就OK了：
	<id>nexus-aliyun</id>
	<mirrorOf>central</mirrorOf>
	<name>Nexus aliyun</name>
	<url>http://maven.aliyun.com/nexus/content/groups/public</url>

###通过字节流的方式读取文件时出现乱码问题？###

	通过转换流转换成字符流，因为转换流构造器中可以设置默认的编码集编码集，字节流不可以。
	InputStreamReader(is,"GBK") 输入转换流 -- 转换成GBK编码
		InputStreamReader 是字节流通向字符流的桥梁(转换流)
		OutputStreamWriter 是字符流通向字节流的桥梁：(转换流)
	BufferedReader br = new BufferedReader(new InputStreamReader(is,"GBK"));

###JSP页面数据传递中文乱码###

	<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
	**<!-- 第一行不要忘记加这个是解决乱码问题 -->**

###ajax请求获得的数据如何传递给外部变量?###

	ajax增加属性，并设置为false（默认为true）
	"cache": false, 
	"async": false,
	**不在异步 同步了**

###Spring MVC中的JSON 数据传输###

	生成JSON数据 （对象或字符串） 
	方法上添加注解 @ResponseBody 访问url可以直接显示json数据
	1、使用HuTool 
	JSONObject json1 = JSONUtil.createObj();
		json1.put("longitude", longitude);
		json1.put("latitude", latitude);
		return json1.toString();
	**网站源码**
	F:\personage\whyTedu\eclipse-workspace\IPMVC\src\main\java\edu\mvcdemo\controller\ReturnJsonController.java
	**eclipse-workspace IPMVC项目中有jsonObject数据增加，传递等方法测试实例**
	*只能传递字符串 无法传递对象 什么问题呢？ 需要研究*

###net.sf.json-lib jar包导入报错？###

	是因为JDK版本的问题，所以需要在加一句指定jdk版本
	<dependency>
		    <groupId>net.sf.json-lib</groupId>
		    <artifactId>json-lib</artifactId>
		    <version>2.4</version>
		    `<classifier>jdk15</classifier>`
	</dependency>

###Shell 是如何连接用户和内核的？###

		Shell 能够接收用户输入的命令，并对命令进行处理，处理完毕后再将结果反馈给用户，比如输出到显示器、写入到文件等，这就是大部分读者对 Shell 的认知。你看，
	我一直都在使用 Shell，哪有使用内核哦？我也没有看到 Shell 将我和内核连接起来呀？！
		其实，Shell 程序本身的功能是很弱的，比如文件操作、输入输出、进程管理等都得依赖内核。我们运行一个命令，大部分情况下 Shell 都会去调用内核暴露出来的接口，
	这就是在使用内核，只是这个过程被 Shell 隐藏了起来，它自己在背后默默进行，我们看不到而已。
		接口其实就是一个一个的函数，使用内核就是调用这些函数。这就是使用内核的全部内容了吗？嗯，是的！除了函数，你没有别的途径使用内核。
		比如，我们都知道在 Shell 中输入cat log.txt命令就可以查看 log.txt 文件中的内容，然而，log.txt 放在磁盘的哪个位置？分成了几个数据块？在哪里开始？
	在哪里终止？如何操作探头读取它？这些底层细节 Shell 统统不知道的，它只能去调用内核提供的 open() 和 read() 函数，告诉内核我要读取 log.txt 文件，请帮助我，
	然后内核就乖乖地按照 Shell 的吩咐去读取文件了，并将读取到的文件内容交给 Shell，最后再由 Shell 呈现给用户（其实呈现到显示器上还得依赖内核）。整个过程中
	Shell 就是一个“中间商”，它在用户和内核之间“倒卖”数据，只是用户不知道罢了。

###Shell 还能连接其它程序###

		在 Shell 中输入的命令，有一部分是 Shell 本身自带的，这叫做内置命令；有一部分是其它的应用程序（一个程序就是一个命令），这叫做外部命令。
		Shell 本身支持的命令并不多，功能也有限，但是 Shell 可以调用其他的程序，每个程序就是一个命令，这使得 Shell 命令的数量可以无限扩展，其结果就是 Shell 
	的功能非常强大，完全能够胜任 Linux 的日常管理工作，如文本或字符串检索、文件的查找或创建、大规模软件的自动部署、更改系统设置、监控服务器性能、发送报警邮件、
	抓取网页内容、压缩文件等。
		更加惊讶的是，Shell 还可以让多个外部程序发生连接，在它们之间很方便地传递数据，也就是把一个程序的输出结果传递给另一个程序作为输入。
		大家所说的 Shell 强大，并不是 Shell 本身功能丰富，而是它擅长使用和组织其他的程序。Shell 就是一个领导者，这正是 Shell 的魅力所在。
		可以将 Shell 在整个 Linux 系统中的地位描述成下图所示的样子。注意“用户”和“其它应用程序”是通过虚线连接的，因为用户启动 Linux 后直接面对的是 Shell，
	通过 Shell 才能运行其它的应用程序。

##HTTP协议##

	HTTP协议:超文本传输协议
	浏览器与服务端之间传输数据的协议，底层的传输协议为TCP。
	HTTP则为应用层协议，负责定义传输数据的格式。

	HTTP协议分为1.0与1.1两个版本。现在常用为1.1版本。

	协议规定客户端与服务端通讯方式为:一次请求一次响应
		即:客户端发起请求，服务端接收到请求后向客户端发送响应。
		服务端不会主动发送内容给客户端。采取"一问一答"的形式。

	HTTP对请求与响应分别定义了格式。并且，无论是请求还是
	响应中发送的字符(不含正文部分内容)都只能符合**ISO8859-1**
	编码字符(如:数字，字母，符号)。像中文等其他字符都需要
	经过处理后才可以发送。

	HTTP请求格式
	一个HTTP请求分为三部分组成:请求行，消息头，消息正文

	**1:请求行**
	请求行分为三部分:
	请求方法 资源路径 协议(CRLF)  
	method url protocol(CRLF)
		例如:
		GET /index.html HTTP/1.1(CRLF)

	请求行以CRLF结束
	CR:回车符,asc编码中对应数字13
	LF:换行符,asc编码中对应数字10

	**2:消息头**
	消息头由若干行表示，每行表示一个具体的头信息
	每个头信息格式分为两部分:
	消息头名字:消息头的值(CRLF)
	name:value(CRLF)
	每个消息头都以CRLF结尾。
	最后一个消息头结尾处会有两个CRLF，第一个表示最后一个
	消息头结束，第二个表示消息头部分结束。
		例如:
		Host: localhost:8080(CRLF)
		Connection: keep-alive(CRLF)
		Cache-Control: max-age=0(CRLF)
		Upgrade-Insecure-Requests: 1(CRLF)
		User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.106 Safari/537.36(CRLF)
		Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8(CRLF)
		Accept-Encoding: gzip, deflate, sdch(CRLF)
		Accept-Language: zh-CN,zh;q=0.8(CRLF)(CRLF)

	**3:消息正文**
	正文部分不是必须部分，消息正文是2进制数据。是客户端在发送请求时发送给服务端客户提交的数据。这些数据可能是注册信息，上传的图片等。具体数据是什么类型以及这些2进制数据有多少字节会在消息头中具体说明。若消息头中
	没有说明消息正文内容则这个请求中是不含有正文的。

	##下面是浏览器发送给服务端的一个请求(不含有正文部分)##

	GET /index.html HTTP/1.1CRLF
	Host: localhost:8080
	Connection: keep-alive
	Cache-Control: max-age=0
	Upgrade-Insecure-Requests: 1
	User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.106 Safari/537.36
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
	Accept-Encoding: gzip, deflate, sdch
	Accept-Language: zh-CN,zh;q=0.8
	
	###HTTP响应###

	HTTP响应格式也分为三部分:状态行，响应头，响应正文
	
	###状态行格式:###

	protorol status-code status-reason
	协议版本 状态码 状态描述
	
	###状态代码有五类:###

	1xx:信息响应类，表示接受到请求并继续处理
	2xx:处理成功响应类,表示动作被成功接收兵处理
	3xx:重定向类，为了完成指定的动作，必须接受下一步处理
	4xx:客户端错误类，表示客户端请求包含错误的语法或不能
	        正确的执行
	5xx:服务端错误类，服务端不能正确的处理一个正确的请求。    
	常见的:
	200:一切正常
	302:服务端要求客户端重定向到指定路径
	404:用于请求资源未找到
	500:服务端处理异常
	
	
	###响应头格式:###

	响应头的格式与请求中的消息头格式一致。
	
	
	###响应正文:###

	响应正文也是二进制数据，用于将客户端请求的资源等
	信息发送回给客户端。该正文具体表示的介质类型以及占用
	的字节长度会在响应头中有所描述。
	
	
	###一个HTTP响应大致内容:###

	HTTP/1.1 200 OK(CRLF)
	Content-Type:text/html(CRLF)
	Content-Length:224586(CRLF)(CRLF)
	1101010101001.....2进制字节数据

##常用算法##

###冒泡排序###

	public void bubbleAlor(int[] data) {
 
		int temp;
		for (int i = 0; i < data.length; i++) {
 
			for (int j = 0; j < data.length - i - 1; i++) {
				if (data[j] > data[j + 1]) {
					temp = data[j];
					data[j] = data[j + 1];
					data[j + 1] = temp;
				}
			}
		}
	}

###选择排序###

	public void chooseSeq(int[] data) {
 
		for (int i = 0; i < data.length; i++) {
			int min = i;
			for (int j = i + 1; j < data.length; j++) {
				if (data[min] > data[j]) {
					min = j;
				}
			}
 
			if (min != i) {
				int temp = data[min];
				data[min] = data[i];
				data[i] = temp;
			}
		}
	}

###二分法查找###

	public static int search(int[] arr, int key){
        int start=0;
        int end=arr.length-1;
        while (start<=end)
        {
            int mid = (end+start)/2;
            if (key<arr[mid])
            {
                end=mid-1;
            }else if (key>arr[mid]){
                start=mid+1;
            }else {
                return mid;
            }
        }
        return -1;
    }
###找出数组中的最小值###

	private static int findMin(int array[]){

		int min=Integer.MAX_VALUE;//int类型能表示的最大值
		for(int e:array){
			if(e<min)min=e;  
		}
		return min;
	}

###求数组之和###

	private static int addAll(int array[]){  

		int sum=0;  
		for (int i=0; i < array.length; i++){  
			sum+=array[i];  
		}  
		return sum;   
	} 

###JsonArray遍历的方法###

	如果接送JsonObject中有JsonArray
	使用：String data = str.substring(str.indexOf("["),str.indexOf("]")+1);
	或者：JSONObject jsonObject = JSONObject.fromObject(str); 
		 String data = jsonObject.get("data").toString();
	获取	[{name；xxx,age:xxx...}] 格式的字符串
		data// 一个未转化的字符串
	// 首先把字符串转成 JSONArray  对象
	JSONArray array = JSONArray.fromObject(data);
    	if (array.size()>0) {
			for(int i = 0;i<array.size();i++) {
				// 遍历 jsonarray 数组，把每一个对象转成 json 对象
				JSONObject job = array.getJSONObject(i);
				// 得到 每个对象中的属性值
				System.out.println(job.get("femalename"));
			}
		}

###JsonObject遍历的方法###

	JSONObject jsonObject = new JSONObject(s);
	//然后用Iterator迭代器遍历取值，建议用反射机制解析到封装好的对象中
	JSONObject jsonObject = new JSONObject(jsonString);
	        Iterator iterator = jsonObject.keys();
	while(iterator.hasNext()){
	            key = (String) iterator.next();
	        value = jsonObject.getString(key);
	}

###EXT JS中 将时间戳渲染成指定的日期格式(时间戳与时间格式互转)

	--时间戳转时间格式
	renderer:function (value) {
		return Ext.util.Format.date(new Date(parseInt(value)),
		'Y-m-d H:i:s')
	}
	--时间格式转时间戳
	time 为生成的日期选择器
	new Date(time.getValue()).getTime();	

###EXT JS中 获取store数据

	Ajax 获取到数据 
	root属性的赋值为获取到的数据
	 //tmp = ds.data.items[0].data.age; //这个也可以
       var tmp = schemeStore.getAt(0).get("iid");
	//iid 为root获取到的数据的属性 **不可以直接get root获取到的数据

### EXT JS中 使用Store渲染columns(某一列:方案名称)

	{
			text : '方案名称',
			flex : 1,
			dataIndex : 'ischemeid',
			renderer:function (value) {//schemeStore渲染方案名称
				var totalCount = schemeStore.totalCount;
				for(var i = 0;i<totalCount;i++){
					var tmp = schemeStore.getAt(i).get("iid");
					if(value == tmp){
						return schemeStore.getAt(i).get("iname");
					}
				}
			}
		}

###windows 10 开机启动项修改技巧

	--添加开机启动项法一
	可以通过添加启动文件夹的启动项的方式来实现程序开机自启动，具体路径有：
	C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp和
	C:\Users\%username%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup,
	复制这个两个路径到文件浏览器地址栏按下回车键，把想要开机启动的程序的快捷方式放到其中一个文件夹即可
	--添加开机启动项法二
	可以通过注册表来添加系统开机启动项，具体位置在注册表的路径:HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run,
	然后在右侧窗口中点击右键，选择“新建 - 字符串值”，把新值重命名为开机启动项的名称，再双击该值打开“编辑字符串”窗口，把“数值数据”填写为
	开机启动项的路径即可

###Windows根据端口号查找对应服务,并且Kill掉对应服务，（端口占用）

	--在命令窗口中输入命令中输入netstat -ano |findstr “端口号”
	netstat -ano|findstr "3306"
	--查看到对应的进程id之后，就可以通过id查找对应的进程名称
	tasklist |findstr "4636"
	--在命令框中输入如下命令taskkill /f /t /im “进程id或者进程名称”
	taskkill /f /t /im "4636"

###commons-lang常用方法

	跟java.lang这个包的作用类似，Commons Lang这一组API也是提供一些基础的、通用的操作和处理，如自动生成toString()的结果、自动实现hashCode()
	和equals()方法、数组操作、枚举、日期和时间的处理等等。

	lang包主要是一些可以高度重用的Util类； 
	lang.enum已不建议使用，替代它的是紧随其后的lang.enums包; 
	lang.enums包顾名思义用于处理枚举； 
	lang.builder包包含了一组用于产生每个Java类中都常使用到的toString()、hashCode()、equals()、compareTo()等等方法的构造器； 
	lang.exception包用于处理Java标准API中的exception，为1.4之前版本提供Nested Exception功能； 
	lang.math包用于处理数字； 
	lang.mutable用于包装值型变量； 
	lang.time包提供处理日期和时间的功能。
	
	Commons的包和类很多，这些包和和类的常见用法可以在用到时参考一下Javadoc，位置就在安装路径的		
		…/commons-lang-2.1/docs/api/index.html

###commons.lang包下的静态util类###

	在org.apache.commons.lang包中提供了一些有用的包含static方法的Util类。除了6个Exception类和2个已经deprecated的数字类之外，commons.lang包共包含了17个实用的类：
	
	ArrayUtils – 用于对数组的操作，如添加、查找、删除、子数组、倒序、元素类型转换等；
	
	BitField – 用于操作位元，提供了一些方便而安全的方法；
	
	BooleanUtils – 用于操作和转换boolean或者Boolean及相应的数组；
	
	CharEncoding – 包含了Java环境支持的字符编码，提供是否支持某种编码的判断；
	
	CharRange – 用于设定字符范围并做相应检查；
	
	CharSet – 用于设定一组字符作为范围并做相应检查；
	
	CharSetUtils – 用于操作CharSet；
	
	CharUtils – 用于操作char值和Character对象；
	
	ClassUtils – 用于对Java类的操作，不使用反射；
	
	ObjectUtils – 用于操作Java对象，提供null安全的访问和其他一些功能；
	
	RandomStringUtils – 用于生成随机的字符串；
	
	SerializationUtils – 用于处理对象序列化，提供比一般Java序列化更高级的处理能力；
	
	StringEscapeUtils – 用于正确处理转义字符，产生正确的Java、JavaScript、HTML、XML和SQL代码；
	
	StringUtils – 处理String的核心类，提供了相当多的功能；
	
	SystemUtils – 在java.lang.System基础上提供更方便的访问，如用户路径、Java版本、时区、操作系统等判断；
	
	Validate – 提供验证的操作，有点类似assert断言；
	
	WordUtils – 用于处理单词大小写、换行等。

###使用PL/SQL连接别人的Oracle###

	Oracle 安装目录下 instantclient_11_2 目录  tnsnames.ora 文件进行编辑 
	根据需求修改
	ORCL =
	  	(DESCRIPTION =
	    (ADDRESS = (PROTOCOL = TCP)(HOST = 90.16.0.2)(PORT = 1521))
	    (CONNECT_DATA =
	      (SERVER = DEDICATED)
	      (SERVICE_NAME = orcl)
	    )
  	)

###ORA-12154: TNS: 无法解析指定的连接标识符 - 解决方案###

	1.检查服务
		出现这种问题，首先我们想到的是检查服务有没有问题OracleOraDb11g_home2TNSListener。在运行中输入services.msc，
	打开服务窗口，看看OracleOraDb11g_homeTNSListener这个服务是否正在运行，如果没有运行，则启动。
	2.使用SQL PLUS测试连接。
		如果还有问题，我们使用SQL PLUS测试是否能够连接。运行输入cmd,在命令提示符窗口中输入：
		sqlplus sys/密码@数据库SID as sysdba
		eg：sqlplus sys/abc123@orcl as sysdba
	--`如果可以连接，问题就好办了，说明我们数据库实例是没问题的，问题应该出在oracle客户端和pl/sql developer的配置上。`
	3.查询tnsnames.ora 编辑问题：
	**注意SID名前面不能有任何其他字符，尤其是空格！**
	保存后，看看能不能登录。如果还不行，在pl/sql developer的登录窗口中点“取消”按钮，进入pl/sql developer后，
	执行“工具”-> “首选项” -> 连接，按下图所示进行配置（其中oracle主目录就是oracle客户端的路径）。

###新创建的spring boot项目，pom.xml文件第一行报错###

	现象：如上图所示，pom.xml第一行报错，Problems显示有error。

	原因：Spring Boot 2.1.5.RELEASE默认使用maven-jar-plugin的版本是3.1.2，但是这个版本存在某种bug，导致项目异常，详情可以查看eclipse官网介绍。
	
	解决方案：回退maven-jar-plugin至3.1.1版本。
	
	具体方法：在pom.xml里的properties属性中添加以下代码段即可
	<properties>
	    <java.version>1.8</java.version>
	    <maven-jar-plugin.version>3.1.1</maven-jar-plugin.version>
	</properties>
###EXT JS中 注意各Store的先后顺序###

	EXT JS 中从上到下依次顺序，如果需要用到的store数据尽量放到最前面，以防后面获取不到，一顿Undefined - -

###EXT JS中获取摸store的全部值

	想要获取store的全部值，在store默认有分页值(25)，需要设置pageSize : 1000, 设置的值应大于store的全部数据条数，不然只可以获取分页值的数据条数


###EXT JS中定时任务###

	updateTask = {
         run : function() {
                 updateUserList();
         },
         interval : 2000         // 2 second
	}

###EXT JS字符串替换（变量替换）###

	把 a 替换成 b：	
		string.replace("a","b");  
	以上只能替换第一个匹配的，要全文匹配应该用正则表达式：
		string.replace(/a/g,"b");	正则加个参数 g ，表示全文匹配。

	变量不可以直接匹配正则，并且 JS 里没有 replaceAll() 这个方法----？？？怎么办呢
	JS 里面正则表达式的另一个使用方法，那就是：
		string.replace(new RegExp(key,'g'),"b");
	这里，利用 JS 的 RegExp 对象，将 g 参数单拿了出来，同时，正则的内容可以用变量来代替了！！！！!

###PL/SQL各种窗口的作用###

- PW（程序窗口）:
  `可以执行 sql,sqlplus 相关的语句，例如存储过程，方法，一般用来开发程序用的。`
- TW（测试窗口）:
  `一般是用来测试存储过程等的debug。`
- SW（SQL窗口）:
  `执行的是dml,ddl语句,主要用户语句的查询、显示、执行统计信息等（应用最多的一个窗口）。例如 - desc table不能在SQL window中执行，必须在Command window中才能执行。`
- RW（报告窗口）:
  `方便用于展示有聚合查询的用图表形式展示的窗口，例如sum(),count()等，有x,y轴的。`
- CW（命令窗口）:
  `除了可以执行sql/sqlplus 相关的命令、sql脚本，还可以执行更多的命令，例如call 等。`
- EPW（解释计划窗口）:
  `解释执行计划的，调优时，经常用到。`
-
DW（图表窗口）:
##浅谈数据库之存储过程##

###什么是存储过程###

	如果你接触过其他的编程语言，那么就好理解了，存储过程就像是方法一样。
	竟然他是方法那么他就有类似的方法名，方法要传递的变量和返回结果，所以存储过程有存储过程名有存储过程参数也有返回值。

###存储过程的优点：###

-	`存储过程的能力大大增强了SQL语言的功能和灵活性。`
-	`可保证数据的安全性和完整性。`
-	`通过存储过程可以使没有
-
-	的用户在控制之下间接地存取数据库，从而保证数据的安全。`
-	`通过存储过程可以使相关的动作在一起发生，从而可以维护数据库的完整性。`
-	`在运行存储过程前，数据库已对其进行了语法和句法分析，并给出了优化执行方案。这种已经编译好的过程可极大地改善SQL语句的性能。`
-	`可以降低网络的通信量。`
-	`使体现企业规则的运算程序放入数据库服务器中，以便 集中控制。`
     **存储过程可以分为系统存储过程、扩展存储过程和用户自定义的存储过程**

###系统存储过程##

		我们先来看一下系统存储过程，系统存储过程由系统定义，主要存放在MASTER数据库中，名以"SP"开头或以"XP"开头。尽管这些系统存储过程在MASTER数据库中，
	但我们在其他数据库还是可以调用系统存储过程。有一些系统存储过程会在创建新的数据库的时候被自动创建在当前数据库中。

	####常用系统存储过程有：####

	1、exec sp_databases; --查看数据库
	2、exec sp_tables;        --查看表
	3、exec sp_columns student;--查看列
	4、exec sp_helpIndex student;--查看索引
	5、exec sp_helpConstraint student;--约束
	6、exec sp_helptext 'sp_stored_procedures';--查看存储过程创建定义的语句
	7、exec sp_stored_procedures;
	8、exec sp_rename student, stuInfo;--更改表名
	9、exec sp_renamedb myTempDB, myDB;--更改数据库名称
	10、exec sp_defaultdb 'master', 'myDB';--更改登录名的默认数据库
	11、exec sp_helpdb;--数据库帮助，查询数据库信息
	12、exec sp_helpdb master;
	13、exec sp_attach_db --附加数据库
	14、exec sp_detach_db --分离数据库

###存储过程语法###

在创建一个存储过程前，先来说一下存储过程的命名，看到好几篇讲存储过程的文章都喜欢在创建存储过程的时候加一个前缀，养成在存储过程名前加前缀的习惯很重要，虽然这只是一件很小的事情，但是往往小细节决定大成败。看到有的人喜欢这样加前缀，例如proc_名字。也看到这加样前缀usp_名字。前一种proc是procedure的简写，后一种sup意思是user procedure。我比较喜欢第一种，那么下面所有的存储过程名都以第一种来写。至于名字的写法采用骆驼命名法。

创建存储过程的语法如下：

	CREATE PROC[EDURE] 存储过程名 
	@参数1 [数据类型]=[默认值] [OUTPUT] 
	
	@参数2 [数据类型]=[默认值] [OUTPUT]
	
	AS 
	
	SQL语句
	
	EXEC 过程名[参数]

###使用存储过程实例###

####1.不带参数####

	create procedure proc_select_officeinfo--(存储过程名)
	as select Id,Name from Office_Info--(sql语句)
	
	exec proc_select_officeinfo--(调用存储过程)

####2.带输入参数####

	create procedure procedure_proc_GetoffinfoById --(存储过程名)
	@Id int--(参数名 参数类型)
	as select Name from dbo.Office_Info where Id=@Id--(sql语句)
	
	exec procedure_proc_GetoffinfoById 2--(存储过程名称之后,空格加上参数,多个参数中间以逗号分隔)
	
	注:参数赋值是,第一个参数可以不写参数名称,后面传入参数,需要明确传入的是哪个参数名称

####3.带输入输出参数####

	create procedure proc_office_info--（存储过程名）
	@Id int,@Name varchar(20) output--(参数名 参数类型)传出参数要加上output
	as 
	begin
	select @Name=Name from dbo.Office_Info where Id=@Id --(sql语句)
	end
	declare @houseName varchar(20) --声明一个变量,获取存储过程传出来的值
	exec proc_office_info--(存储过程名)--调用存储过程
	4,@houseName output--(传说参数要加output 这边如果用@变量 = OUTPUT会报错，所以换一种写法)
	select @houseName--(显示值)

####4.带返回值的####

	create procedure proc_office_info--（存储过程名）
	@Id int--(参数名 参数类型)
	as 
	begin
	if(select Name from dbo.Office_Info where Id=@Id)=null --(sql语句)
	begin
	return -1
	end
	else
	begin
	return 1
	end
	end
	
	declare @house varchar(20) --声明一个变量,获取存储过程传出来的值
	exec @house=proc_office_info 2 --(调用存储过程,用变量接收返回值)
	--注：带返回值的存储过程只能为int类型的返回值
	print @house

###gv格式文本文件转换成图片（png格式）###

	dot D:\test\1.gv -Tpng -o image.png

###Eclipse环境安装rust###

	在run configure 中 build command 下输入
	${CARGO_TOOL_PATH} build

### Oarcle中的oracle中blob,clob,nclob类型主要区别是什么？ ###

	1、在Oracle中，LOB（Large Object，大型对象）类型的字段现在用得越来越多了。因为这种类型的字段，容量大（最多能容纳4GB的数据），且一个表中可以有多个这种类型的字段，很灵活，
	适用于数据量非常大的业务领域（如图象、档案等）。
	2、LOB类型分为BLOB和CLOB两种：BLOB即二进制大型对象（Binary Large Object），适用于存贮非文本的字节流数据（如程序、图象、影音等）。
	3、而CLOB，即字符型大型对象（Character Large Object），则与字符集相关，适于存贮文本型的数据（如历史档案、大部头著作等）。

	BLOB全称为二进制大型对象（Binary Large Object)。它用于存储数据库中的大型二进制对象。可存储的最大大小为4G字节
	CLOB CLOB全称为字符大型对象（Character Large Object)。它与LONG数据类型类似，只不过CLOB用于存储数据库中的大型单字节字符数据块，不支持宽度不等的字符集。可存储的最大大小为4G字节
	NCLOB 基于国家语言字符集的NCLOB数据类型用于存储数据库中的固定宽度单字节或多字节字符的大型数据块，不支持宽度不等的字符集。可存储的最大大小为4G字节
	BFILE 当大型二进制对象的大小大与4G字节时，BFILE数据类型用于将其存储在数据库外的操作系统文件中；当其大小不足4G字节时，则将其存储在数据库内部的操作系统文件中，BFILE列存储文件定位程序，此定位程序指向服务器上的大型二进制文件。

###查看当前有哪些用户正在使用数据###

	select osuser, a.username, cpu_time/executions/1000000||'s', b.sql_text, machine from v$session a, v$sqlarea b where a.sql_address =b.address order by cpu_time/executions desc;

### Rust racer补全工具编译错误 解决方法###

	错误信息：：may not be used on the stable release channel
	将rust 变成 黑暗模式  哈哈哈哈！！
		rustup default nightly

### PhantomReference  vs WeakReference ###

	PhantomReference  有两个好处， 
	其一， 它可以让我们准确地知道对象何时被从内存中删除， 这个特性可以被用于一些特殊的需求中(例如 Distributed GC，  XWork 和 google-guice 中也使用 PhantomReference 做了一些清理性工作).
	其二， 它可以避免 finalization 带来的一些根本性问题, 上文提到 PhantomReference 的唯一作用就是跟踪 referent 何时被 enqueue 到 ReferenceQueue 中,  但是 WeakReference 也有对应的功能, 两者的区别到底在哪呢 ? 
	这就要说到 Object 的 finalize 方法, 此方法将在 gc 执行前被调用, 如果某个对象重载了 finalize 方法并故意在方法内创建本身的强引用,  这将导致这一轮的 GC 无法回收这个对象并有可能 
	引起任意次 GC， 最后的结果就是明明 JVM 内有很多 Garbage 却 OutOfMemory， 使用 PhantomReference 就可以避免这个问题， 因为 PhantomReference 是在 finalize 方法执行后回收的，也就意味着此时已经不可能拿到原来的引用,  也就不会出现上述问题,  当然这是一个很极端的例子, 一般不会出现. 

### 如何保存 Windows 10「聚焦」功能的精美壁纸 ###

	访问：
	%localappdata%\Packages\Microsoft.Windows.ContentDeliveryManager_cw5n1h2txyewy\LocalState\Assets
	复制文件到指定文件夹，当前文件夹执行 ren * *.jpg

### 在命令行执行DB2 存储过程文件/ ###

	**连接数据库**

	连接数据库 db2 connect to entegor1

	**DB2执行脚本**

		*1、执行sql语句脚本文件*
		（1）db2 -tvf *.sql，此命令执行*.sql脚本中间出现错误不断开；
		（2）db2 -txvf *.sql，此命令执行*.sql脚本中间出现错误会断开，，并提示错误；
		
		*2、执行DB2存储过程脚本文件 ($ 结束符) *
		db2 -td$ -vf *.sql
		db2 -td$ -f 

	db2 -td@ -f <SQL过程文件路径> -l <输出日志文件路径>
	
	**MySQL执行脚本**
	source <SQL过程文件路径>

### 在字符串中指定字符串第一次出现的位置，插入xxx ###


		StringBuffer sbu = new StringBuffer();
        sbu.append("Hello World");
        System.out.println(sbu);
		System.out.println(sbu.indexOf("H"));
        sbu.insert(sbu.indexOf("H")+1, "xxx");
        System.out.println(sbu);

### Oracle 数据库的关联条件字段可拼接###

	下面是使用：拼接两个字段
	H.IP=(A.IAGENT_IP||':'||A.IAGENT_PORT))

### 修改字段类型sql脚本 ###

	--oracle
	ALTER TABLE IEAI_FSH_TASK MODIFY (IAUDITOR VARCHAR2(4000))
	
		SELECT SIGN(COUNT(*)) INTO LI_EXISTS FROM USER_TAB_COLUMNS WHERE TABLE_NAME='IEAI_FSH_TASK' AND COLUMN_NAME='IAUDITOR';
			IF LI_EXISTS = 1 THEN 
				LS_SQL := 'ALTER TABLE IEAI_FSH_TASK MODIFY (IAUDITOR VARCHAR2(4000))';
				EXECUTE IMMEDIATE LS_SQL;
			END IF;
	
	
	--DB2
	ALTER TABLE IEAI_FSH_TASK ALTER COLUMN IAUDITOR SET DATA TYPE VARCHAR(4000)
	
	SELECT	SIGN(COUNT(*)) INTO LI_EXISTS FROM SYSCAT.COLUMNS WHERE TABNAME='IEAI_FSH_TASK' AND  COLNAME='IAUDITOR';
			IF	LI_EXISTS = 1 THEN
				SET LS_SQL = 'ALTER TABLE IEAI_FSH_TASK ALTER COLUMN IAUDITOR SET DATA TYPE VARCHAR(4000)';
				PREPARE SQLA FROM LS_SQL; 
				EXECUTE SQLA;
	END IF;
	
	
	--mysql
	ALTER  TABLE IEAI_FSH_TASK CHANGE IAUDITOR IAUDITOR VARCHAR(4000)
	
	IF EXISTS (SELECT * FROM INFORMATION_SCHEMA.COLUMNS WHERE  TABLE_NAME = 'IEAI_FSH_TASK' AND COLUMN_NAME = 'IAUDITOR') THEN
			ALTER TABLE IEAI_FSH_TASK MODIFY IAUDITOR VARCHAR(4000) ;
	END IF;

### extjs grid监听事件 获取值 ###

		 listeners: {
             cellclick: function (grid, rowIndex, columnIndex, e) {
            	 var itype = grid.getHeaderAtIndex(4).dataIndex;
            	 var itypeDate = e.get(itype);
            	 console.log('====>itype',itype)
            	 console.log('====>itypeDate',itypeDate)
                 /*var fileName = grid.getHeaderAtIndex(columnIndex).dataIndex;//列名
                 var data = e.get(fileName);//单元格value
                 var list = ['1', '2', '3', '4', '5', '6', '7', '8', 'S', 'Q'];
                 if (list.indexOf(data) >= 0) {
                     var flightdataNum = grid.getHeaderAtIndex(0).dataIndex;//当前行的第一列列名
                     var segmentNum = grid.getHeaderAtIndex(1).dataIndex;
                     var flightNONum = grid.getHeaderAtIndex(2).dataIndex;
                     var flightDate = e.get(flightdataNum);//当前行的第一列列值
                     var segment = e.get(segmentNum);
                     var flightNO = e.get(flightNONum);
                     updateData(fileName, flightDate, segment, flightNO, data);
                 }*/
             }
         }

### eclipse 运行项目java.lang.OutOfMemoryError: PermGen space ###

	修改虚拟机参数为：
		（Debug Configurations）

		-Xms1024M -Xmx2048M -XX:PermSize=128M -XX:MaxPermSize=256M

		-Xms，表示程序启动时，JVM 堆的初始化最小尺寸参数；
		-Xmx，表示程序启动时，JVM 堆的初始化最大尺寸参数；
		-XX:PermSize，表示程序启动时，JVM 方法区的初始化最小尺寸参数；
		-XX:MaxPermSize，表示程序启动时，JVM 方法区的初始化最大尺寸参数。

	本例中的错误，实际上，只需要扩展方法区的虚拟机参数即可。

### SQL 分组统计 没有的如何显示为0  ###

	原因是执行group by之前，已经先执行where条件筛选了。当时脑袋就一直被绕进这两个先后顺序的弯里，出不来。百度了好久，都没有结果，最后还是询问了几个同学才搞出来。
	
	思路是这样的，先对通过新闻类型ID对新闻信息表MessageInfo进行统计分组，返回一个包含新闻类型ID和新闻数量的新集合，然后左连接到新闻类型表MessageType中。这个时候就基本上完成了。那些没有新闻类型下没有新闻信息的左连接后就是null，最后我们把null用isnull()函数替换成0就可以。sql语句如下：
	
	1 select a.MessageName as '新闻类型',isnull(b.count,0) as '新闻数量' from MessageType as a
	2 left join(
	3 select MessageTypeId,count(1) as [count] from MessageInfo group by MessageTypeId) as b 
	4 on a.MessageTypeId=b.MessageTypeId

### HSSF，XSSF，SXSSF ###

	HSSF：Excel97-2003版本，扩展名为.xls。一个sheet最大行数65536，最大列数256。
	
	XSSF：Excel2007版本开始，扩展名为.xlsx。一个sheet最大行数1048576，最大列数16384。
	
	SXSSF：是在XSSF基础上，POI3.8版本开始提供的支持低内存占用的操作方式，扩展名为.xlsx。
	
	作者：帮我的鸵鸟盖个章
	链接：https://www.jianshu.com/p/c8766986b95b
	来源：简书
	著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


### TIMESTAMP类型查询 ###

	2019-3-11 上午11:43:15

	Oracle：
	SELECT
	* 
	FROM
		IEAI_TIMETASK_RUNTIME 
	WHERE
		STARTTIME >=TO_TIMESTAMP( '2020-03-02 02:36:11','yyyy-mm-dd hh24:mi:ss.ff')

	DB2：
	SELECT
	* 
	FROM
		IEAI_TIMETASK_RUNTIME 
	WHERE
		STARTTIME >=TIMESTAMP( '2020-03-02 02:36:11')

	MYSQL：
	SELECT
	* 
	FROM
		IEAI_TIMETASK_RUNTIME 
	WHERE
		STARTTIME >=str_to_date( '2020-03-02 02:36:11','%Y-%m-%d %H:%i:%s')


### ext js 比较Store中的值，并获取（以前都是获取到value发送.do请求，消耗太多资源） ###

	if (value != '') {
           var index = dataCenterStore.findExact("iid", value);
           if (index != -1) {
                 backValue = dataCenterStore.getAt(index).data.iname;
           } 
    }

###数据库字段拼接比较###

	eg：192.168.0.111：15000（） 与 192.168.0.111 比较
	//只比较了IP 进行拆分后比较
	oracle
	 	WHERE SUBSTR (H.IP, 0, INSTR (H.IP, ':', 1, 1) - 1) = A.IAGENT_IP
	DB2
		WHERE SUBSTR(IP, 1, LOCATE(':', IP)-1) = A.IAGENT_IP
	mysql
		WHERE（SELECT SUBSTRING_INDEX (H.IP, ':' , 1)FROM IDUAL）= A.IAGENT_IP

###修改字段长度命令###

	1.mysql
	修改字段长度命令
	alter table 表名 modify column 列名 类型(要修改的长度);
	alter table bank_branch_number modify column bankId varchar(10);
	2.
	修改字段的语法：alter table tablename modify (column datatype [default value][null/not null],….);
	alter table test1 modify (name varchar2(16) default 'unknown');
	3.db2 
	ALTER table 【table】alter column 【column】 set data type VARCHAR(50);
	
	**已有数据修改，修改的类型数据不符合原始类型，使用以下方法**
	SELECT SIGN(COUNT(*)) INTO LI_EXISTS FROM USER_TAB_COLUMNS WHERE TABLE_NAME='IEAI_ACTFINISHED_FLAG_NEW' AND COLUMN_NAME='IDATADATE' AND TYPENAME<>'VARCHAR';
   	IF LI_EXISTS != 0 THEN
    LS_SQL := 'ALTER TABLE IEAI_ACTFINISHED_FLAG_NEW ADD DES NUMBER(19)';
        EXECUTE IMMEDIATE LS_SQL;
        LS_SQL := 'UPDATE IEAI_ACTFINISHED_FLAG_NEW SET DES=IDATADATE';
        EXECUTE IMMEDIATE LS_SQL;
        LS_SQL := 'UPDATE IEAI_ACTFINISHED_FLAG_NEW SET IDATADATE=NULL';
        EXECUTE IMMEDIATE LS_SQL;
        LS_SQL := 'ALTER TABLE IEAI_ACTFINISHED_FLAG_NEW MODIFY  IDATADATE VARCHAR(255)';
        EXECUTE IMMEDIATE LS_SQL;
        LS_SQL := 'UPDATE IEAI_ACTFINISHED_FLAG_NEW SET IDATADATE=DES';
        EXECUTE IMMEDIATE LS_SQL;
        LS_SQL := 'ALTER TABLE IEAI_ACTFINISHED_FLAG_NEW DROP (DES)';
    EXECUTE IMMEDIATE LS_SQL;
    COMMIT;
	END IF;

### Oracle 存储过程 in、out、in out 参数的使用方法 ###
	1、in 参数
		用于接收参数，在子程序内部，不能进行修改。默认的参数模式：in
			--定义打印的存储过程
			CREATE OR REPLACE PROCEDURE println (str VARCHAR)
			AS
			BEGIN
			  dbms_output.put_line(str);
			  END;
			--定义测试in模式的存储过程
			CREATE OR REPLACE PROCEDURE pro(p1 IN INT,p2 IN INT)--参数的个数、类型可以自定义，但是参数不允许指定长度
			AS
			BEGIN
			  println(p1);
			  println(p2);
			  --p2:=11; --in模式参数不能为其赋值
			  END;
			
			--通过语句块调用存储过程
			BEGIN
			  pro(10,100);
			  END;

	2、out模式参数 
		输出模式的参数，用于输出值，会忽略传入的值。在子程序内部可以对其进行修改。 
		输出：子程序执行完毕后，out模式参数最终的值会赋值给调用时对应的<实参变量>。 
		注意：out模式参数的调用，必须通过变量。
			--测试out模式的存储过程
			CREATE OR REPLACE PROCEDURE pro(p3 OUT INT)
			AS
			BEGIN
			  println(p3);--p3会忽略传入的值
			  p3:=33;--设定存储过程调用后的值
			  END;
			
			DECLARE
			var3 INT :=30;--声明一个变量用于设定存储过程调用前的值
			BEGIN
			-- pro(30); --error,20对应过程中out模式的参数，out会输出结果给调用的实参，但是20不能作为赋值目标
			println('存储过程调用前的值：'||var3);
			pro(var3);--调用pro存储过程重新赋值；调用过程，如果过程形参是out模式，必须采用变量实参
			println('存储过程调用后的值：'||var3);
			  END;

	3、in out 模式参数 
		输入输出模式：能接收传入的实参值；在子程序内部可以修改； 可以输出（必须用实参变量调用）
			--测试in out模式的存储过程
			CREATE OR REPLACE PROCEDURE pro(p4 IN OUT INT)
			AS
			BEGIN
			  println(p4);
			  p4:=44;--in out模式参数的值可以修改
			  END;
			
			DECLARE
			var4 INT :=40;--声明一个变量用于设定存储过程调用前的值
			BEGIN
			println('存储过程调用前的值：'||var4);
			pro(var4);--调用pro存储过程重新赋值
			println('存储过程调用后的值：'||var4);
			  END;

### Oracle函数汇总 ###

	Oracle函数将近100种

	select [测试函数] from dual	

	单行函数：（字符串函数、数字函数、日期函数、转换函数）

		1、字符串函数
			ASCII(X)==========================================返回字符X的ASCII码
			CHR(X)============================================根据数字代码返回字符,反函数ASCII()
			CONCAT(X,Y)=======================================连接字符串X和Y
			INSTR(X,STR,[START],[N])==========================从X中查找str第一次出现的位置，可以指定从start开始，也可以指定从n开始
			INSET('helloworld','l',2,2)=======================返回结果：4 在"helloworld"的第2(e)号位置开始，查找第二次出现的“l”的位置
			INSETB('helloworld','l',2,2)======================按照字节算
			LENGTH(X)=========================================返回X以字符为单位的长度.  LENGTHB(X)返回X以字节为单位的长度
			VSIZE(X)==========================================返回自己数
			LOWER(X)==========================================X转换成小写
			UPPER(X)==========================================X转换成大写
			INITCAP(X)========================================X第一个字母变为大写;
			LTRIM('helloworld','hello')=======================返回结果：world 从左边截取，会截空格，缺省去空白
			RTRIM('helloworld','world')=======================返回结果：hello 从右边截取，会截空格，缺省去空白
			TRIM('o' FROM 'ohelloworldo')=====================返回结果：helloworld 从两边截取，会截空格，缺省去空白
			REPLACE(X,old,new)================================在X中查找old，并替换成new（匹配的是整个字符串）
			TRANSLATE(X, old, new)============================old 是 abc new 是123 那么只要X中有a就替换成1，有b就2。。（匹配的是单个字符）
			SUBSTR(X,start,[length])==========================返回X的字串，从start处开始，截取length个字符，缺省length，默认到结尾
			SUBSTRB(X,start,[length])=========================按照字节算
			CONVERT(string1, char_set_to ,[char_set_from] )==将字符串从一个字符集转换为另一个字符集,char_set_to：要转换为的字符集。char_set_from：可选的，要从中转换的字符集。
			LPAD(X, padded_length, [pad_X] )=================函数从左边对字符串使用指定的字符进行填充,X被填充字符串，padded_length填充后长度如果小于总长度从左到右截取，pad_X填充的字符串
			RPAD(X, padded_length, [pad_X] )=================与上面相同从右
			LTRIM(X,[n])=====================================将字符串X从左的第n个位置去空白   RTRIM(X,[n]) 从右
			SOUNDEX(X)=======================================返回字符串参数的语音表示形式????
			TO_MULTI_BYTE(c1)================================将字符串中的半角转化为全角
			TO_SINGLE_BYTE(c)================================将字符串中的半角转化为半角


		2、数字函数
			ABS(X)============================================X的绝对值	ABS(-3)=3
			ACOS(X)===========================================X的反余弦	ACOS(1)=0
			COS(X)============================================余弦 COS(1)=0.54030230586814
			COSH(X)===========================================反余弦
			CEIL(X)===========================================大于或等于X的最小值 CEIL(5.4)=6
			FLOOR(X)==========================================小于或等于X的最大值 	FLOOR(5.8)=5
			LOG(X,Y)==========================================X为底Y的对数 LOG(2，4)=2
			MOD(X,Y)==========================================X除以Y的余数 MOD(8，3)=2
			POWER(X,Y)========================================X的Y次幂 POWER(2，3)=8
			ROUND(X[,Y])======================================X在第Y位四舍五入 ROUND(3.456，2)=3.46 
			SQRT(X)===========================================X的平方根 SQRT(4)=2
			TRUNC(X[,Y])======================================X在第Y位截断 TRUNC(3.456，2)=3.45
			LN(X)=============================================返回数字X(X必须大于0)的自然对数
			SIGN(X)===========================================函数返回X一个数字的正负标志. 正数1 负数0 0即0

				说明：【 ROUND(X[,Y]) TRUNC(X[,Y]) 】
				ROUND(X[,Y]) 在缺省 y 时，默认 y=0；比如：ROUND(3.56)=4。四舍五入
				TRUNC(X[,Y]) 在缺省 y 时，默认 y=0；比如：ROUND(3.56)=3。直接取整，全入
				y 是正整数，就是四舍五入到小数点后 y 位。ROUND(5.654,2)=5.65。
				y 是负整数，四舍五入到小数点左边|y|位。ROUND(351.654,-2)=400。

		3、日期函数
			SYS_DATE===数据库系统时间

			ADD_MONTHS(d,n)===================================在某一个日期 d 上，加上指定的月数 n，返回计算后的新日期。
				SQL：SELECT SYSDATE,add_months(SYSDATE,5) FROM dual;
				输出结果：2020/4/10 19:47:08 | 2020/9/10 19:47:08

			LAST_DAY(d)=======================================返回指定日期当月的最后一天。
				SQL：ELECT SYSDATE,last_day(SYSDATE) FROM dual;
				输出结果：2020/4/10 19:47:08 | 2020/4/30 19:47:08	

			ROUND(d[,fmt])====================================返回一个以 fmt 为格式的四舍五入日期值， d 是日期， fmt 是格式模型。默认 fmt 为 DDD，即月中的某一天。
				① 如果 fmt 为“YEAR”则舍入到某年的 1 月 1 日，即前半年舍去，后半年作为下一年。
				② 如果 fmt 为“MONTH”则舍入到某月的 1 日，即前月舍去，后半月作为下一月。
				③ 默认为“DDD”，即月中的某一天，最靠近的天，前半天舍去，后半天作为第二天。
				④ 如果 fmt 为“DAY”则舍入到最近的周的周日，即上半周舍去，下半周作为下一周周日。
				SQL：SELECT SYSDATE,ROUND(SYSDATE),ROUND(SYSDATE,'day'),ROUND(SYSDATE,'month'),ROUND(SYSDATE,'year') FROM dual;	
				输出结果：1	2020/4/10 19:52:01 | 2020/4/11 | 2020/4/12 | 2020/4/1 | 2020/1/1
			
			TRUNC(d[,fmt])==================================== TRUNC 与 ROUND 非常相似，只是不对日期进行舍入，直接截取到对应格式的第一天

			EXTRACT(fmt FROM d)===============================提取日期中的特定部分。
				fmt 为：YEAR、MONTH、DAY、HOUR、MINUTE、SECOND。其中 YEAR、MONTH、DAY可以为 DATE 类型匹配，也可以与 TIMESTAMP 类型匹配；但是 HOUR、MINUTE、SECOND 必须与 TIMESTAMP 类型匹配。
				**HOUR 匹配的结果中没有加上时区，因此在中国运行的结果小 8 小时。**
				SQL：SELECT SYSDATE as "data" ,EXTRACT(YEAR FROM SYSDATE) "year",EXTRACT(MONTH FROM SYSDATE)"month",
					EXTRACT(DAY FROM SYSDATE)"day",EXTRACT(HOUR FROM SYSTIMESTAMP)"hour",
					EXTRACT(MINUTE FROM SYSTIMESTAMP)"minute",EXTRACT(SECOND FROM SYSTIMESTAMP)"second" FROM dual
				输出结果：2020/4/10 20:00:35	| 2020 | 4 | 10 | 12 | 0 | 35.879424

			MONTHS_BETWEEN (date1, date2)=====================用于返回date1和date2之间有几个月

			NEW_TIME(DATE, time_zone1, time_zone2)============将一个日期和时间值从一个时区转换到另外一个时区。

			NEXT_DAY(date,char)===============================date时间下一个星期几（char）char也可用1～7替代,还可以是星期一、星期二。。。星期日 
			
		4、转换函数
			TO_CHAR(d|n[,fmt])================================把日期和数字转换为制定格式的字符串。Fmt是格式化字符串
				SQL：SELECT TO_CHAR(SYSDATE,'YYYY"年"MM"月"DD"日" HH24:MI:SS')"date" FROM dual;
				输出结果：	2020年04月10日 20:05:27
				
				SQL:SELECT TO_CHAR(-123123.45,'L9.9EEEEPR')"date" FROM dual
				输出结果：	<￥1.2E+05>
				
			TO_DATE(X,[fmt])==================================把一个字符串以fmt格式转换成一个日期类型

			TO_NUMBER(X,[fmt])===============================把一个字符串以fmt格式转换为一个数字
				SQL:SELECT TO_NUMBER('-$12,345.67','$99,999.99')"num" FROM dual;
				输出结果：	-12345.67

			
		
		5、其它单行函数
			NVL(X,VALUE)======================================如果X为空，返回value，否则返回X
			NVL2(x,value1,value2)=============================如果x非空，返回value1，否则返回value2
	
	聚合函数：
		聚合函数同时对一组数据进行操作，返回一行结果，比如计算一组数据的总和，平均值等。
		AVG(表达式)===平均值 
		SUM(表达式)===求和 
		MIN(表达式)===最小值 
		MAX(表达式)===最大值 
		COUNT(表达式)===数据统计
		MEDIAN(表达式)===中间值 
		VARIANCE(表达式)===方差 
		STDDEV(表达式)===标准差


	不常用函数：
		三角函数：
		SIN(x)==================返回x的正弦，其中x为弧度值
		ASIN(X)=================返回x的反正弦，即正弦x的值，若x不在-1到1的范围内，则返回NULL
		ACOS(X)=================返回x的反余弦，即余弦x的值，若x不在-1到1的范围内，则返回NULL
		ATAN(X)=================返回x的反正切，即正切x的值
		ATAN2(X,Y)==============正切是X /Y的以弧度表示的角
		
		BFilename===============用于返回一个BFILE定位器，这个定位器指向一个物理的LOB二进制文件。
			其中directory是指一个目录对象，该目录对象对应该文件的全路径，该文件位于文件服务器上。
			filename 是指该文件在文件服务器上文件名。
			eg：创建一个叫exampleDir目录对象，该目录对象指向文件服务器的路径/example/totn.
				CREATE DIRECTORY exampleDir AS '/example/totn';
				后我们可以在bfilename函数中使用exampleDir目录对象:
				SELECT bfilename('exampleDir', 'totn_logo.jpg') FROM dual;

		CHARTOROWID(string)=====将字符数据类型转换为ROWID类型,把包含外部格式的ROWID的CHAR或VARCHAR2数值转换为内部的二进制格式.参数string必须是包含外部格式的ROWID的18字符的字符串.oracle7和oracle8中的外部格式是不同的.CHARTOROWID是ROWIDTOCHAR的反函数.
			在数据库中每一行记录都有一个地址，你可以通过查询伪列ROWID来查看该值。
		ROWIDTOCHAR(ROWID)======与CHARTOROWID(string)是反函数
		
		DEREF()=================输出ref对象时候使用，（面向对象引用。指针概念）
		REF()===================创建ref对象时候使用   MAKE_REf()这个函数不知道是干嘛的。。。。  RefToHex（）转为为十六进制？？
			ORACLE在关系数据库外，融入了面向对象的元素,比如可以创建type，type之间可以继承，type可以带构造函数、排序函数、各种各样的成员函数、存储过程等等
			对象表是指该表的一行就是一个对象，有一个OID(object ID)，对象表之间没有主外键关联的概念，为了体现这层关系，oracle中用了ref对象来实现。

			EG：创建一个地址类型，一个人员类型，人员有地址属性，所以在人员类型中设置一个ref address来确定指向他所在地址的指针。
			--创建地址类型
				SQL：create type address as object(street varchar2(35),city varchar2(15),state char(2),zip_code integer);
			--创建地址对象表
				SQL：create table addresses of address;
			--创建人员类型
				SQL：create type person as object(first_name varchar2(15),last_name varchar2(15),birthday date,
					  home_address ref address, --指向对应的地址，该地址应该在另外一个对象表中的一行
					  phone_number varchar2(15));
			--创建人员对象表
				SQL：CREATE TABLE persons of person;
			--插入一个地址
				SQL：insert into addresses values(address('nanhai','shenzhen','gd','518054'));
				SQL：insert into addresses values(address('shennan','shenzhen','gd','518057'));
			--插入一个人员，注意这里的home_address部分是如何插入一个ref address的。通过ref（）函数获取地址对象表中某一行的引用，用来创建人员对象表的ref地址
				SQL：insert into persons values(person('shitou','haha',to_date('1982-07-05','yyyy-mm-dd'),
					(select ref(a) from addresses a where street='nanhai'),'1355555555'));
			--也可使用存储过程来是实现插入一个人员记录
				declare
				  addref ref address ;
				begin
				  select ref(a) into addref from addresses a where street='nanhai';
				  insert into persons
				    values (person('shitou','haha',to_date('1982-07-05','yyyy-mm-dd'),
				                     addref,'1355555555'));
				  commit;
				end;
			 --查询某人的地址信息
				SQL：select first_name,deref(home_address) from persons;
			 --修改地址
				SQL：update persons set home_address=(select ref(a) from addresses a where street='shennan');
			 --删除某个人员
				SQL：delete from persons where first_name='shitou';
			--删除某个地址的相关人员记录
				SQL：delete from persons where home_address=(select ref(a) from addresses a where street='nanhai');

		DUMP(expr[,return_fmt[,start_position][,length]])========数据类型检测函数，可以检测Orcle中的数据类型，返回type（类型对应码值） len（所占字节数）
		   type码值：1      VARCHAR2
					2      NUMBER
					8      LONG
					12     DATE
					23     RAW
					24     LONG RAW
					69     ROWID
					96     CHAR
					112    CLOB
					113    BLOB
					114    BFILE
					180    TIMESTAMP
					181    TIMESTAMP WITH TIMEZONE
					182    INTERVAL YEAR TO MONTH
					183    INTERVAL DAY TO SECOND
					208    UROWID
					231    TIMESTAMP WITH LOCAL TIMEZONE

		Empty_BLOB()=============================|
		Empty_CLOB()=============================|-没有找到对应解释，应该是对BLOB与CLOB类型进行空验证。
		EXP(x)=================================== exp(sum(字段)) 字段乘积

		GREATEST(expr_1, expr_2, ...expr_n)======函数从表达式（列、常量、计算值）expr_1, expr_2, ... expr_n等中找出最大的数返回。在比较时，OracIe会自动按表达式的数据类型进行比较，以expr_1的数据类型为准。
		LEAST(expr_1, expr_2, ...expr_n)=========与上面想反，找出最小的数返回。
		
		GROUPING()===============================GROUPING函数可以接受一列，返回0或者1。如果列值为空，那么GROUPING()返回1；如果列值非空，那么返回0
		GROUPING只能在使用ROLLUP或CUBE的查询中使用。
		
		ROLLUP()=================================是GROUP BY子句的一种扩展，可以为每个分组返回小计记录以及为所有分组返回总计记录。
		CUBE()===================================是GROUP BY子句的一种扩展，可以返回每一个列组合的小计记录，同时在末尾加上总计记录。

		hextoraw(X)==============================十六进制字符串转换为raw	
		rawtohex(X)==============================将raw串转换为十六进制
			下面是常用到了两个函数：
			utl_raw.cast_to_raw([varchar2]);--将varchar2转换为raw类型
			utl_raw.cast_to_varchar2([raw]);--将raw转换为varchar2类型

		NLS 字符函数返回关于字符集的信息
			NLS_charset_decl_len(bytecnt, csid)
			NLS_charset_id(csid)
			NLS_charset_name(n)
			NLS_initcap(char, nlsparam)
			NLS_lower(char, nlsparam)
			NLS_upper(char, nlsparam)
			NLSSort(char, nlsparam)

		SYS_CONTEXT('USERENV','多选参数')========查询系统环境信息
			select sys_context('USERENV','terminal') 当前会话终端标识符,
	        sys_context('USERENV','language') 语言,
	        sys_context('USERENV','db_name') 当前的数据库实例名称,
	        sys_context('USERENV','session_user') 当前会话的数据库,
	        sys_context('USERENV','current_schema')  查看当前方案 from dual;
			等等等。。。。。

		SYS_GUID()==============================获取序列号

		UID=====================================当前用户的唯一整数

		USER====================================当前用户

		USERENV(parameter)======================当前会话上下文
			Isdba:若用户具有dba权限，则返回true,否则返回false.
			
			Language:返回当前会话对应的语言、地区和字符集。
			
			LANG:返回当前环境的语言的缩写
			
			Terminal:返回当前会话所在终端的操作系统标识符。
			
			Sessionid:返回正在使用的审计会话号.
			
			Client_info:返回用户会话信息，若没有则返回null.

###数据库中SQL Union和SQL Union All用法###

	UNION 指令的目的是将两个 SQL 语句的结果合并起来， union只是将两个结果联结起来一起显示，并不是联结两个表
	我们用 UNION这个指令时，我们只会看到不同的资料值 (类似 SELECT DISTINCT)--没有重复数据。	
	UNION ALL 这个指令的目的也是要将两个 SQL 语句的结果合并在一起，
	UNION ALL 和 UNION 不同之处在于 UNION ALL 会将每一笔符合条件的资料都列出来，无论资料值有无重复。--有重复数据


### 数组输出 ###

	System.out.println(Arrays.toString(arr));

---

### redhat 6.5 安裝配置eclipse ###

	可能会提示 GTK+ 版本低====》升级GTK+ 使用yum在线安装GTK+

	１.yum在线安装gtk
    １）pkg-config -version查看pkg-config的版本（本机测试是0.25）
    ２）安装必要组建：（在root权限下）yum install gtk2 gtk2-devel gtk2-devel-docs 
    ３）可能还需要组建（可选，不行再装）：yum install gnome-devel gnome-devel-docs
    ４）有些linux版本已经自带了gtk包，需要安装yum install gtk2-devel
    ５）安装成功后通过pkg-config --modversion gtk+-2.0查看gtk版本（本机测试是2.24.13）
    ６）在线安装的好处就是不需要自己处理依赖关系，但是对于学习来说，未必是一件好事。	

	可能还会提示无法找到java虚拟机===》
	查看jdk是否安装   java -version javac -version
	如果jdk已经安装 
	修改eclipse 根目录下 eclipse.ini 文件 
	第一行添加如下两行：
	-vm
	/usr/local/java/jdk1.7.0_79/jre/bin（ 这一行为jdk安装目录）


### 表格模板 ###

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |


### sql 处理数据字段为空 如何为空转换成别的值 ###

	1.oracle : 
	nvl(“字段名”，’转换后的值’)；//字段名是双引号，转换后的值是单引号 
	2.sql Server: 
	isnull(“字段名”,’转换后的值’)//字段名是双引号，转换后的值是单引号 
	3.mySql: 
	ifnull(字段名，’转换后的值’)//字段名不加引号，转换后的值是单引号



### 数据库数据查询、相同数据去重关键字 ###

	select DISTINCT * from ieai_user 

### EXT JS grid 重新加载数据 ###

	Ext.getCmp("ttaudtitaskinfo_grid").ipage.doRefresh();
	Ext.getCmp("ttaudtitaskinfo_grid").store.reload();

### PL\SQL 理解执行计划 ###

	1.全表扫描(full table scans)：这种方式会读取表中的每一条记录，顺序地读取每一个数据块直到结尾标志，对于一个大的数据表来说，使用全表扫描会降低性能，但有些时候，比如查询的结果占全表的数据量的比例比较高时，全表扫描相对于索引选择又是一种较好的办法。
    2.通过ROWID值获取(table access by rowid)：行的rowid指出了该行所在的数据文件，数据块及行在该块中的位置，所以通过rowid来存取数据可以快速定位到目标数据上，是oracle存取单行数据的最快方法。
    3.索引扫描(index scan)：先通过索引找到对象的rowid值，然后通过rowid值直接从表中找到具体的数据，能大大提高查找的效率。

### 使用instr函数 按照某个字段 规定顺序排序 ###

	eg：使用instr函数 将ISTATE字段按照指定的0,30,10,11排序
	特定情况下order by/order by decs 无法满足要求
	stateOrder = " order by instr('0,30,10,11',ISTATE)";

### 数据库表暂挂状态###

	错误码： DB2 SQL Error: SQLCODE=-668, SQLSTATE=57016

	解决办法:CALL SYSPROC.ADMIN_CMD('reorg table 表名')    reorg  table  :是对表结构进行重组刷新!

### Oracle 参数 processes、sessions设置 ###

	1.登录服务器 export ORACLE_SID=xxx（登录具体实例，需要先设置SID）
	2.su - oracle
	3.sqlplus sys as sysdba(回车)  提示输入密码的时候在(回车)
	4.查看参数 select * from v$resource_limit 
	5.修改参数 alter system set processes = 2000 scope = spfile;
	6.关闭数据库  shutdown immediate
	7.启动数据库 Startup
	8.退出当前用户 exit
	9.监听数据库 lsnrctl start

### poi 解析excel 浮点数跟整数的读取 ###

	Double d = cell.getNumericCellValue();  
	DecimalFormat df = new DecimalFormat("#.##");  
	String value = df.format(d);


### web项目启动报错###
	严重：Servlet.service() for servlet [jsp] threw exception
	ClassNotFoundException: # Licensed to the Apache Software Foundation (ASF) under one or more

	【jar包冲突，看第一行，servlet-api.jar 冲突】

### Oracle 锁 ###
	select session_id from v$locked_object

	SELECT sid, serial#, username, osuser FROM v$session where sid = 101

	ALTER SYSTEM KILL SESSION 'sid,serial#'
	
	========================根据表名查询================================
	select c.sid, c.serial#, c.username, c.osuser, b.owner, b.object_name, a.locked_mode, p.spid from v$locked_object a, dba_objects b, v$session c, v$process p where a.object_id = b.object_id  and a.session_id = c.sid  and c.paddr = p.addr and b.object_name = '表名'  --查询锁表

	alter system kill session 'sid, serial#' ;--填写对应的sid, serial#
	

	ORACLE里锁有以下几种模式:
	0：none
	1：null 空
	2：Row-S 行共享(RS)：共享表锁，sub share 
	3：Row-X 行独占(RX)：用于行的修改，sub exclusive 
	4：Share 共享锁(S)：阻止其他DML操作，share
	5：S/Row-X 共享行独占(SRX)：阻止其他事务操作，share/sub exclusive 
	6：exclusive 独占(X)：独立访问使用，exclusive
	
	数字越大锁级别越高, 影响的操作越多。
	
	1级锁有：Select，有时会在v$locked_object出现。
	2级锁有：Select for update,Lock For Update,Lock Row Share 
	select for update当对话使用for update子串打开一个游标时，所有返回集中的数据行都将处于行级(Row-X)独占式锁定，其他对象只能查询这些数据行，不能进行update、delete或select for update操作。
	3级锁有：Insert, Update, Delete, Lock Row Exclusive
	没有commit之前插入同样的一条记录会没有反应, 因为后一个3的锁会一直等待上一个3的锁, 我们必须释放掉上一个才能继续工作。
	4级锁有：Create Index, Lock Share
	locked_mode为2,3,4不影响DML(insert,delete,update,select)操作, 但DDL(alter,drop等)操作会提示ora-00054错误。
	00054, 00000, "resource busy and acquire with NOWAIT specified"
	// *Cause: Resource interested is busy.
	// *Action: Retry if necessary.
	5级锁有：Lock Share Row Exclusive 
	具体来讲有主外键约束时update / delete ... ; 可能会产生4,5的锁。
	6级锁有：Alter table, Drop table, Drop Index, Truncate table, Lock Exclusive



### 局域网下共享， 数据库连接 ###

	关闭服务所在电脑防火墙
	# 123 改为你的数据库密码
	# mysql
	grant all privileges on *.* to root@"%" identified by '123' with grant option; 
	flush privileges;
	# oracle

	更改本地的 tnsnames.ora配置文件，添加本地IP地址。
	默认安装路径： H:\app\Administrator\product\11.2.0\dbhome_1\NETWORK\ADMIN\tnsnames.ora
	// 添加一条本地IP的描述，HOST填充本机的IP地址
	ORCL =
	  (DESCRIPTION =
	    (ADDRESS = (PROTOCOL = TCP)(HOST = 192.168.0.104)(PORT = 1521))
	    (CONNECT_DATA =
	      (SERVER = DEDICATED)
	      (SERVICE_NAME = orcl)
	    )
	  )

### db2 数据库实例重启 ###
		1.查看是否有活动的链接
			db2 list applications for db db_name
		2.关闭连接
			db2 force application all
		4.执行停止实例命令
			命令：db2stop
		5.执行实例启动命令
			命令：db2start
		6.如果此时，发现连接不了数据库，莫慌，需要激活目标数据库
	
	　　首先查看是否有活跃的数据库
	　　	命令：db2 list active databases
	　　如果没有，需要对目标数据库进行激活设置
	　　	命令：db2 activate database db_name
	
	　　然后再次使用上一条命令，就可查看到当前已有活跃的数据库了，此时可进行连接并执行数据库操作。

### 修改Linux 主机名影响DB2数据库启动的问题 ###

	SQL6031N 在 db2nodes.cfg 文件的行号"1" 上出错。原因码为"10"。

	Linux 主机名称修改： vi /etc/sysconfig/network  vi /etc/hosts 修改两处，只修改一处会影响DB2启动不解决报错的问题。
	DB2 <修改数据库实例下>/sqllib/db2nodes.cfg 配置文件，将名称修改为主机名称

	更改三处配置文件后，重启

	重新启动 reboot -> su - 数据库用户 -> 启动数据库db2 db2start ->  db2 connect to 数据库实例名

### Java 8 新特性 Lambda 表达式遍历 List Map ###

	遍历Map
	Map<String, String> map = new HashMap<String, String>() {{
            put("a", "A");
            put("b", "B");
            put("d", "D");
            put("c", "C");
    }};
	// map key k  / map value v
    map.forEach((k, v) -> {
         System.out.print("key=" + k);
         System.out.print("\t");
         System.out.println("value=" + v);
    });


	遍历List  //item 为list中元素 <T>
	list.forEach(item->{

	});

### win10彻底永久关闭自动更新的方法 ###

	一、通过服务禁用 Windows Update服务

	1、通过services.msc 命令禁用 Windows Update服务
	2、换到“恢复”选项，将默认的“重新启动服务”改为“无操作”，然后点击“应用”“确定”
![](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrEA.Qs.LZ*l7i5rN.3HqF*i1bVXOy2JhTSu9LLwuNXO*brM1ZKm6u0ILlP6*JuyuBxwut6hqC8qrc6xzBpodVZQw!/b&bo=2AFWAgAAAAADF78!&rf=viewer_4)

	二、可以通过配置组策略来关闭Windows系统的自动更新。
	
	1、输入命令：gpedit.msc，打开配置组策略。

	2、找到计算机配置下的【管理模板】，然后找到设置下的【Windows组件】
![Alt](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrEAy6bLFKDoe0WcaI*JVkcXvw9THK0dTzjIWbwEb5B9ltOKrUw0iMrXVTIzgYQhSthFVu8xFLsJVObTg4c83mXiM!/b&bo=rgOfAQAAAAADFwE!&rf=viewer_4)

	3、然后找到Windows组件下的【Windows更新】
![Alt](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrELgiNyZljuRznWEwwlX.gcEg5P4eTaSpD3wgzeyrBo1f0BcMfpgOwLWhyd8J..G0QUOgMeMJi7f*MarQ4BK6bD4!/b&bo=pwO5AQAAAAABFyw!&rf=viewer_4)

	4、然后点击进入Windows更新，找到右边的【配置自动更新】
![Alt](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrEPbEcp0.d4Azh9fUv3YkMO9QYnb0dfvSfCjKc8iYBDepaVikqqiX3IAIQz.IlvAzO8SXo0DcBCVVGILY6CuGkPM!/b&bo=0AJSAQAAAAABF7E!&rf=viewer_4)

	5、然后双击鼠标进入配置自动更新属性，把【已禁用】选项勾上，按确定，即可关闭Windows自动更新了。
![Alt](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrEG2hMOj*BPuDiLHZUi1I8aU6sTai4*3ItWp9ZiVQLvJcGe98PpK9Os1ogozoe8eI6Lt423go42LM822UUfv9t3M!/b&bo=0AKOAQAAAAABF20!&rf=viewer_4)

	三、禁用任务计划里边的Win10自动更新
	1、命令 taskschd.msc

	2、在任务计划程序的设置界面，依次展开 任务计划程序库 -> Microsoft -> Windows -> WindowsUpdate，
	把里面的项目都设置为 [ 禁用 ] 就可以了。（我这里边只有一个任务，你的电脑里可能会有2个或者更多，全部禁用就行了）

![](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrEHD78CpcTioqoenPfpQXUourCsLXNgBih1Lv3jQ8rV*J1UfuSVq9S5puL9SXpD7Zp9hlNxzs.2KoDtLINV6.QG0!/b&bo=KgKNAQAAAAABF5Q!&rf=viewer_4)

	四、在注册表中关闭Win10自动更新
	1、命令 regedit
	
	2、在注册表设置中，找到并定位到 [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\UsoSvc]。然后在右侧找到“Start”键。
![](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrELExA8805CA9rSOv5x77M72SrZmLdczO..*pA5k*OfUwGsrtVDISgF5q4g3dY10jNK41bpXCfDDc4WppD3qt8rA!/b&bo=KQLKAQAAAAABF9A!&rf=viewer_4)

	3、点击修改，把start值改成16进制，值改为“4”，然后点击「 确定 」保存数据，如图所示。

	4、继续在右侧找到“FailureActions”键，右键点击修改该键的二进制数据，将“0010”、“0018”行的左起第5个数值由原来的“01”改为“00”，完成后，点击下方的“确定”即可，如下图所示。
![](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrEOm.XlFZ*i3lb2L.gbN9aRgcDENlAjWuFH9HzXFKwN4TgWaYBYHhJ91TBs8gE4g7ZjuDCZdq8m9RbifoUlxiMjk!/b&bo=KgJ4AQAAAAABF2E!&rf=viewer_4)

### 数据库备份表 ###

	create table cd_name_new as (select * from cd_name) definition only;-----复制表结构
	insert into cd_name_new (select * from cd_name);--------把数据插入到新表


### RESTFul API是REST在Web接口中的应用和延伸 ###

	你知道RESTful API吗？他的优点和缺点是啥？有没有替换方案？

	REST包含三要求，即资源（Resources）、表现层（Representation）、状态转化（State Transfer）
	资源：就是一个网络上的实体，一个链接，一个图片，一个视频，任务网络上的东西，都可以确定为一个资源，URI就是它的地址
	表现层：把资源具体展现中的形式，就叫表现层，比如文本使用txt、html、xml、json格式表现，图片使用jpg、gif、png格式表现
	状态转化：通过操作，使得客户端和服务端对某个资源在表现层上展现出来的不同状态，叫状态转化，而操作的手段，只能是通过HTTP协议，比如用GET、POST、PUT、DELETE请求状态
	
	1、协议 一般是指HTTP或HTTPS协议
	2、域名 https://www.google.com
	3、版本号 google.com/v1/
	4、路径 注意：路径一般使用名词，且为复数，表示一种资源
	5、操作 如：GET、POST、PUT、PATCH、DELETE
	6、过滤 通过一般URL参数，提供数据过滤
	7、状态码
	8、返回结果 根据上面的请求操作与URL，返回特定的JSON结果

	**RESTful的缺点**

	RESTful API毋庸置疑，非常好用、简单且强大，它把任何当成一个资源，非常适合微服务提供的请求返回。

	但随着接口的增多，它也导致了一个问题：过多的接口，就导致接口爆炸，过少的接口，就导致信息臃肿。
	
	前端在请求数据时，其实有时候，需要多个资源的集合，有时候又不需要单个资源的所有数据，前端希望
	能根据我的请求，返回特定的资源数，这时候，RESTful API明显就力不从心了。

	**GraphQL API**
	这时，GraphQL API就派上用场了，完美的解决了上面RESTful API的缺点。

### Oracle存储过程基本语法介绍 ###

[https://cloud.tencent.com/developer/article/1040780](https://cloud.tencent.com/developer/article/1040780 "Oracle存储过程基本语法介绍")

### 创建一个对象 ###

![](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrEIpTBG*zG2sOJiF8K9uwauzy0MJVofsYfVBzKMCnMY7*k.iHU1T7RSDZUNQ2NxEVuhiFz3mEH0DUA6X2pRKOg5Q!/b&bo=uwHoAAAAAAADF2A!&rf=viewer_4)

### Kafka，ActiveMQ，RabbitMQ，RocketMQ有什么优缺点？ ###

![](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrEFAHd3XEnU6j.pUKw*bI2QyfMAEmz5N1hsXqZVxAYRHyRsTrRZp.QYiLvro5XLx6CayVf1pBr3Puy36nXtSV2kU!/b&bo=mwOFAgAAAAADFy0!&rf=viewer_4)

### 消息队列有什么优缺点 ###

	**优点：**
	解耦：生产->MQ->消费
	异步：分发多个请求至MQ,多个MQ服务分别消费
	削峰：生产->积压至MQ->可消费消费

	**缺点：**
	系统可用性降低：单服务MQ挂掉，建立MQ集群
	系统复杂度提高：你怎么保证消息没有重复消费？怎么处理消息丢失的情况？
	一致性问题：A系统处理完了直接返回成功了，人都以为你这个请求就成功了；但是问题是，要是BCD三个系统那里，BD两个系统写库成功了，结果C系统写库失败了，咋整？你这数据就肯定了。


### RMI与RPC的区别 ###

	1、方法调用方式不同：

	RMI调用方法，RMI中是通过在客户端的Stub对象作为远程接口进行远程方法的调用。每个远程方法都具有方法签名。如果一个方法在服务器上执行，但是没有相匹配的签名被添加到这个远程接口(stub)上，那么这个新方法就不能被RMI客户方所调用。

	RPC调用函数，RPC中是通过网络服务协议向远程主机发送请求，请求包含了一个参数集和一个文本值，通常形成“classname.methodname(参数集)”的形式。这就向RPC服务器表明，被请求的方法在“classname”的类中，名叫“methodname”。然后RPC服务器就去搜索与之相匹配的类和方法，并把它作为那种方法参数类型的输入。这里的参数类型是与RPC请求中的类型是匹配的。一旦匹配成功，这个方法就被调用了，其结果被编码后通过网络协议发回。

	2、适用语言范围不同：
	RMI只用于Java，支持传输对象。
	RPC是基于C语言的，不支持传输对象，是网络服务协议，与操作系统和语言无关。

	3、调用结果的返回形式不同：
	RMI是面向对象的，Java是面向对象的，所以RMI的调用结果可以是对象类型或者基本数据类型。
	RPC的结果统一由外部数据表示(External Data Representation,XDR)语言表示，这种语言抽象了字节序类和数据类型结构之间的差异。只有由XDR定义的数据类型才能被传递，可以说RMI是面向对象方式的Java RPC。

### RPC与HTTP ###

	RPC：Remote Produce Call远程过程调用，类似的还有RMI（Remote Methods Invoke 远程方法调用，是JAVA中的概念，是JAVA十三大技术之一）。自定义数据格式，基于原生TCP通信，速度快，效率高。早期的webservice，现在热门的dubbo，都是RPC的典型

	http其实是一种网络传输协议，基于TCP，规定了数据传输的格式。现在客户端浏览器与服务端通信基本都是采用Http协议。也可以用来进行远程服务调用。缺点是消息封装臃肿。

	**相同点：**
	底层通讯都是基于socket，都可以实现远程调用，都可以实现服务调用服务

	**不同点：**
	RPC：框架有：dubbo、cxf、（RMI远程方法调用）Hessian
	当使用RPC框架实现服务间调用的时候，要求服务提供方和服务消费方 都必须使用统一的RPC框架，要么都dubbo，要么都cxf
	
	跨操作系统在同一编程语言内使用
	优势：调用快、处理快

	http：框架有：httpClient
	当使用http进行服务间调用的时候，无需关注服务提供方使用的编程语言，也无需关注服务消费方使用的编程语言，服务提供方只需要提供restful风格的接口，服务消费方，按照restful的原则，请求服务，即可
	
	跨系统跨编程语言的远程调用框架
	优势：通用性强

	**总结：对比RPC和http的区别**
	1 RPC要求服务提供方和服务调用方都需要使用相同的技术，要么都hessian，要么都dubbo
	而http无需关注语言的实现，只需要遵循rest规范
	2 RPC的开发要求较多，像Hessian框架还需要服务器提供完整的接口代码(包名.类名.方法名必须完全一致)，否则客户端无法运行
	3 Hessian只支持POST请求
	4 Hessian只支持JAVA语言


### 国内外优秀公共DNS ###

	国外的9个优秀DNS服务器：
	1.谷歌的公共DNS服务器
	主DNS：8.8.8.8
	辅DNS：8.8.4.4
	谷歌的免费DNS服务器通常被列为最好的，它们易于记忆，并且每个人都可以使用。它甚至可以提供令人印象深刻的速度。
	
	谷歌DNS的主要优势来自他们作为一家公司的声誉。谷歌每年收入极多，有能力提供最稳定和更有弹性的DNS服务器。
	
	这个DNS服务器的唯一问题是它们存储有关您的运营的信息，如果美国政府决定需要这些信息，它们可以与第三方共享。但是，对于不担心此问题的用户，Google通常被认为是最好的DNS服务器。
	
	2. Norton ConnectSafe
	主DNS： 199.85.126.10
	辅DNS： 199.85.127.10
	诺顿以其出色的防病毒，互联网安全服务和产品而闻名。但是，人们不知道他们的DNS服务器也不会令人失望。
	
	该DNS地址可防止恶意软件和诈骗。这是他们可用的三个级别的互联网防护DNS中的第一个。
	
	第2个是199.85.126.20和199.85.127.20，还限制了带有色情内容的网站，第3个是199.85.126.30和199.85.126.30，增加了阻止诺顿认为非家庭友好的内容，如果你很感兴趣，您可以在Norton ConnectSafe - DNS常见问题中找到非家庭友好内容列表。
	
	这些选项使Norton ConnectSafe成为父母的父母可以轻松选择的，这些孩子希望保护他们免受在线不需要的资料的侵害。
	
	3. OpenDNS
	主DNS： 208.67.222.222
	辅DNS： 208.67.220.220
	OpenDNS是今天仍然存在的另一个老竞争对手，是搜索发现的几个最好的DNS服务器列表中另一个常见的候选者。它的质量与Google的DNS效率相当。
	
	同样，对于关心孩子互联网安全的用户，OpenDNS提供了一项名为OpenDNS FamilyShield的服务，可以阻止成人内容（可在服务器208.67.222.123和208.67.220.123获得）。
	
	4. DNS Watch
	主DNS： 84.200.69.80
	辅DNS： 84.200.70.40
	DNS Watch专注于透明度和自由选择，提供最好的DNS服务器，不受任何形式的审查。他们还保证不会在他们的服务器上存储任何信息，并且他们的解析器不会设置为记录您的任何数据。
	
	他们的形象是无私的服务和团队。他们唯一的目的是为每个人提供高效的互联网。他们还声称，他们不是一家大公司，这有助于避免政府监管。所以对于那里的自由爱好者来说，这是一个很好的选择。
	
	此外，为了跟上他们的透明态度，他们甚至还提供免费DNS服务器的实时统计数据。这种透明性使它们成为最佳DNS服务器的良好候选者，至少在可信度和匿名DNS服务器方面。
	
	5. Comodo安全DNS
	主DNS： 8.26.56.26
	辅DNS： 8.20.247.20
	另一个易于设置的服务器。
	
	其中一个有利的一面的科摩多安全DNS是它跨越全球15个节点的事实。在每个大陆上，每个节点包含几个服务器，准备为本地用户提供服务。这使得Comodo Secure DNS成为用户的绝佳选择。
	
	关于DNS服务器速度的许多问题之一是您与其服务器的距离。
	
	无论您身在何处，Comodo的全球报道都能让它快速发展。众所周知，Comodo Secure DNS是最好的DNS服务器之一，因为它还可以让您远离恶意软件和骗局网站。他们会定期更新阻止列表。
	
	以合理的速度进行全球覆盖，再加上它自动检测“未使用”或“重影”页面的事实，使其成为最佳DNS服务器标题的引人注目的选择。特别推荐那些渴望可公开访问且安全的DNS服务器的用户。
	
	6.威瑞信
	主DNS： 64.6.64.6
	辅DNS： 64.6.65.6
	Verisign的服务基于两个主题：作为匿名DNS服务器，并提供恶意软件和恶意网站的保护。
	
	他们特别指出，让客户知道他们不会向第三方出售他们的信息，也不会向用户提供任何广告。
	
	7. OpenNIC
	主DNS： 192.95.54.3
	辅DNS： 192.95.54.1
	OpenNIC是那些不想弄清楚最接近其位置的服务器的用户的绝佳选择。
	
	此处列出的DNS服务器只是它们可用的大量服务器的一部分。如果您访问他们的网站，您不仅可以查找最接近您所在位置的DNS，还可以让该网站自动为您执行此操作。这样你就可以省去寻找最佳DNS的麻烦。
	
	8. GreenTeamDNS
	主DNS： 81.218.119.11
	辅DNS： 209.88.198.133
	有关家庭友好型互联网的最佳DNS服务器的另一名亚军，它不仅会阻止带有色情内容的网站，还会阻止包含恶意软件，僵尸程序以及与暴力和毒品相关的网站。
	
	如前所述，对于父母来说，这尤其有用。
	
	9. Cloudflare DNS
	DNS： 1.1.1.1
	
	由职业的网站安全加速服务提供商cloudflare提供，新发布不久，主打安全、隐私、迅速。自用过cloudflare家的cdn服务，感觉还不错
	
	国内优秀公共DNS服务：
	1、114DNS （http://www.114dns.com/）
		114.114.114.114
		114.114.115.115
	2、腾讯 （https://www.dnspod.cn/Products/Public.DNS）
		119.29.29.29
		182.254.118.118
	3、阿里 （http://alidns.com/）
		223.5.5.5
		223.6.6.6
	4、百度 （http://dudns.baidu.com/intro/publicdns/）
		180.76.76.76
	5、CNNIC （http://www.sdns.cn/）
		1.2.4.8
		210.2.4.8

### 数据库服务启动 ###

	Oracle: 
		[root@vm6-pc186 ~]# su - oracle
		[oracle@vm6-pc186 ~]$ lsnrctl start
		[oracle@vm6-pc186 ~]$ sqlplus /nolog
		SQL> conn /as sysdba
		SQL> startup

	DB2:
		[root@vm6-pc186 ~]# su -bxaoms
		[bxaoms@vm6-pc186 ~]$ db2start
	
	mysql:
		[root@localhost ~]service mysql start

### list 转换成基本类型数组 ###

	long[] JDK1.8特性 
		long [] array = list.stream().mapToLong(t->t.longValue()).toArray();

	Long[] 包装类
		list.toArray(new Long[list.size()])

### 接口分类（http接口、api接口、RPC接口、RMI、webservice、Restful等概念）

	在这之前一定要好好理解一下接口的含义，我觉得在这一类中接口理解成规则很恰当。

        http接口:基于HTTP协议的开发接口.这个并不能排除没有使用其他的协议。

        api接口:API（Application Programming Interface）应用程序编程接口，应用也包括网络应用程序，就像api文档基本上就是使用说明书，API接口可以简单理解成“应用程序使用接口”。

         RPC接口：Remote Procedure Calls 远程过程调用 (RPC) 是一种协议，程序可使用这种协议向网络中的另一台计算机上的程序请求服务。由于使用 RPC 的程序不必了解支持通信的网络协议的情况，因此 RPC 提高了程序的互操作性。在 RPC 中，发出请求的程序是客户程序，而提供服务的程序是服务器。 RPC（远程过程调用）是一项广泛用于支持分布式应用程序（不同组件分布在不同计算机上的应用程序）的技术。RPC 的主要目的是为组件提供一种相互通信的方式，使这些组件之间能够相互发出请求并传递这些请求的结果。 没有语言限制。

        RMI：RMI（Remote Method Invocation，远程方法调用）RMI是针对于java语言的， RMI 允许您使用Java编写分布式对象

        Webservice接口：Webservice是系统对外的接口，比如你要从别的网站或服务器上获取资源或信息，别人肯定不会把数据库共享给你，他只能给你提供一个他们写好的方法来获取数据，你引用他提供的接口就能使用他写好的方法，从而达到数据共享的目的。

        RESTful ： 简称 REST,是描述了一个架构样式的网络系统，其核心是面向资源，REST专门针对网络应用设计和开发方式，以降低开发的复杂性，提高系统的可伸缩性。REST提出设计概念和准则为：

      1.网络上的所有事物都可以被抽象为资源(resource)

      2.每一个资源都有唯一的资源标识(resource identifier)，对资源的操作不会改变这些标识

      3.所有的操作都是无状态的

	关于RPC和RMI的区别，各类博客有很多，我就不说了。Webservice和RESTful ，我不知道你说的是那个（Webservice这个是个大类，包括RESTful ）你可以看看 SOAP Webservice和RESTful Webservice 的区别。不要刻意去混淆找区别，有些是从不同角度、层次而言。也有可能同一个东西兼顾（不同层次、角度的兼顾）。在如今这个软件泛滥的年代，不同的人叫法不同很多，偷换概念的也有很多。http和webservice接口区别
	
	 
	
	http和webservice接口区别
	
	httpservice通过post和get得到你想要的东西
	
	webservice就是使用soap协议得到你想要的东西，相比httpservice能处理些更加复杂的数据类型
	 
	http协议传输的都是字符串了，webservice则是包装成了更复杂的对象。
	
	hessian类似于webservice，但是它采用的是二进制RPC协议（Binary），具有轻量、传输量小、平台无关的特点，特别适合于目前网络带宽比较小的手机网络应用项目。



## 微服务相关 ##


---
###nacos 服务下线配置

![Alt](http://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/TmEUgtj9EK6.7V8ajmQrEL4okCv.vjW7*4TLtxdMxMTqOeNI7iPBGqy6IUUnE*W5RVYpYftlIKv.yAoTcpZVEWlaTCLp1gKqzqHYtV1V0Ck!/b&bo=4QU4BAAAAAADN8o!&rf=viewer_4)

---


## gitHub优秀开源项目 ##

---
`spring boot demo` 是一个用来深度学习并实战 `spring boot` 的项目，目前总共包含 **`66`** 个集成demo

地址：`https://github.com/xkcoding/spring-boot-demo.git`

---
进阶知识完全扫盲：涵盖高并发、分布式、高可用、微服务、海量数据处理等领域知识，特别适合进阶 Java 学习，尤其是工作者

地址：`https://github.com/doocs/advanced-java.git`

---


## Docker ##

### 运行一个容器
	`docker run -it -p 8088:8088 -p 8089:8089 -p 8090:9090 -v /root/soft/docker:/root/soft/docker -v /root/soft/dockertt:/root/soft/dockertt loen/rc /bin/bash`
	
	命令的格式：
	`Usage: docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`
	-a, --attach=[] 登录容器（以docker run -d启动的容器）
	-c, --cpu-shares=0 设置容器CPU权重，在CPU共享场景使用
	--cap-add=[] 添加权限，权限清单详见：http://linux.die.net/man/7/capabilities
	--cap-drop=[] 删除权限，权限清单详见：http://linux.die.net/man/7/capabilities
	--cidfile="" 运行容器后，在指定文件中写入容器PID值，一种典型的监控系统用法
	--cpuset="" 设置容器可以使用哪些CPU，此参数可以用来容器独占CPU
	-d, --detach=false 指定容器运行于前台还是后台
	--device=[] 添加主机设备给容器，相当于设备直通
	--dns=[] 指定容器的dns服务器
	--dns-search=[] 指定容器的dns搜索域名，写入到容器的/etc/resolv.conf文件
	-e, --env=[] 指定环境变量，容器中可以使用该环境变量
	--entrypoint="" 覆盖image的入口点
	--env-file=[] 指定环境变量文件，文件格式为每行一个环境变量
	--expose=[] 指定容器暴露的端口，即修改镜像的暴露端口
	-h, --hostname="" 指定容器的主机名
	-i, --interactive=false 打开STDIN，用于控制台交互
	--link=[] 指定容器间的关联，使用其他容器的IP、env等信息
	--lxc-conf=[] 指定容器的配置文件，只有在指定--exec-driver=lxc时使用
	-m, --memory="" 指定容器的内存上限
	--name="" 指定容器名字，后续可以通过名字进行容器管理，links特性需要使用名字
	--net="bridge" 容器网络设置，待详述
	-P, --publish-all=false 指定容器暴露的端口，待详述
	-p, --publish=[] 指定容器暴露的端口，待详述
	--privileged=false 指定容器是否为特权容器，特权容器拥有所有的capabilities
	--restart="" 指定容器停止后的重启策略，待详述
	--rm=false 指定容器停止后自动删除容器(不支持以docker run -d启动的容器)
	--sig-proxy=true 设置由代理接受并处理信号，但是SIGCHLD、SIGSTOP和SIGKILL不能被代理
	-t, --tty=false 分配tty设备，该可以支持终端登录
	-u, --user="" 指定容器的用户
	-v, --volume=[] 给容器挂载存储卷，挂载到容器的某个目录
	--volumes-from=[] 给容器挂载其他容器上的卷，挂载到容器的某个目录
	-w, --workdir="" 指定容器的工作目录

>> ##详细讲解
### 端口暴露
	-P参数：docker自动映射暴露端口；
	
	`docker run -d -P training/webapp` <span style="color:#009900;">//docker自动在host上打开49000到49900的端口，映射到容器（由镜像指定，或者--expose参数指定）的暴露端口；</span>
	-p参数：指定端口或IP进行映射；
	
	docker run -d -p 5000:80 training/webapp <span style="color:#009900;">//host上5000号端口，映射到容器暴露的80端口；</span>
	docker run -d -p 127.0.0.1:5000:80 training/webapp <span style="color:#009900;">//host上127.0.0.1:5000号端口，映射到容器暴露的80端口；</span>
	docker run -d -p 127.0.0.1::5000 training/webapp <span style="color:#009900;">//host上127.0.0.1:随机端口，映射到容器暴露的80端口；</span>
	docker run -d -p 127.0.0.1:5000:5000/udp training/webapp <span style="color:#009900;">//绑定udp端口；</span>

### 网络配置

	--net=bridge： <span style="color:#009900;">//使用docker daemon指定的网桥</span>
	--net=host： <span style="color:#009900;">//容器使用主机的网络</span>
	--net=container:NAME_or_ID：<span style="color:#009900;">//使用其他容器的网路，共享IP和PORT等网络资源</span>
	--net=none： <span style="color:#009900;">//容器使用自己的网络（类似--net=bridge），但是不进行配置</span>

### Docker 通过容器安装部署DB2数据库

	1，拉取镜像
		（1）首先执行如下命令将镜像下载到本地：
			docker pull ibmcom/db2
		（2）由于镜像比较大（2.96G），执行如下命令删除所有 dangling 数据卷（即无用的 Volume），避免空间不足：
			docker volume rm $(docker volume ls -qf dangling=true)
	2，启动容器 
		（1）执行如下命令实例化 DB2 服务：
			参数说明：
			-d: 表示在后台启动容器；
			-p 50000:50000: 容器内部的 50000 端口映射主机的 50000 端口；
			--name db2：将容器命名为 db2
			--privileged=true：使得容器内的 root 拥有真正的 root 权限。
			-e DB2INST1_PASSWORD=hangge-1234：设置内置实例用户 db2inst1 的密码为 hangge-1234
			-e DBNAME=testdb：容器启动时自动创建一个名为 testdb 的数据库，如果不指定该参数则不创建数据库
			-e LICENSE=accept：接受协议
			-v /usr/local/db2:/database：挂载目录，其中 /usr/local/db2 是宿主机的目录

		docker run -d -it -p50000:50000 --name db2 --privileged=true -e DB2INST1_PASSWORD=1234 -e DBNAME=ideal -e LICENSE=accept -v /usr/local/db2:/database ibmcom/db2
		（2）执行 docker ps 命令确认容器启动成功。
	3，执行命令
		（1）首先执行如下命令进入 DB2 实例的命令环境中：
			docker exec -it db2 bash
		（2）执行如下命令切换到实例用户 db2inst1：
			su - db2inst1
		（3）执行如下命令可以查看运行状态：
			db2pd -
		（4）执行如下命令可以查看数据库和补丁版本：
			db2level
		（5）执行如下命令可以查看已经创建的数据库，可以发现根据启动时的配置参数，目前创建一个 testdb 数据库：
			db2 list db directory
		（6）执行如下命令连接 testdb 数据库：
			db2 connect to testdb
####estart参数=
	no
		默认策略，在容器退出时不重启容器
	on-failure
		在容器非正常退出时（退出状态非0），才会重启容器
	on-failure:3
		在容器非正常退出时重启容器，最多重启3次
	always
		在容器退出时总是重启容器
	开机自启
	unless-stopped
		在容器退出时总是重启容器，但是不考虑在Docker守护进程启动时就已经停止了的容器
	一般推荐使用always参数
	--restart=always


###创建表空间及用户
	创建临时表空间
	create temporary tablespace ideal_temp tempfile '/home/oracle/app/oracle/oradata/helowin/ideal_temp.dbf' size 100m reuse autoextend on next 20m maxsize unlimited;
	
	创建表空间
	create tablespace ideal  datafile '/home/oracle/app/oracle/oradata/helowin/ideal.dbf' size 500M reuse autoextend on next 40M maxsize unlimited default storage(initial 128k next 128k minextents 2 maxextents unlimited);
	
	创建用户并指定表空间
	create user ideal identified by ideal default tablespace ideal  temporary tablespace ideal_temp;
	
	赋予用户权限
	grant dba to ideal;
	
	修改用户名密码
	alter user ideal identified by ideal;


###Oracle 用户密码过期，设置密码永不过期
	1.查看用户的proifle是哪个，一般是default；
	SELECT username,PROFILE FROM dba_users;

	2.查看对应的概要文件(如default)的密码有效期设置（一般默认为180天）;
	SELECT * FROM dba_profiles s WHERE s.profile='DEFAULT' AND resource_name='PASSWORD_LIFE_TIME'
	
	3.将概要文件(如default)的密码有效期由默认的180天修改成“无限制”
	ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED

	4.修改之后不需要重启动数据库，会立即生效

	5.修改后，还没有被提示ORA-28002警告的用户账号不会再碰到同样的提示;而已经被提示的用户账号必须再改一次密码
	alter user 用户名 identified by <原来的密码> account unlock; ----不用换新密码


###Linux 生效配置文件
 	source .bash_profile
###CentOS 7关闭防火墙命令
	1、命令行界面输入命令“systemctl status firewalld.service”并按下回车键。

	2、然后在下方可以查看得到“active（running）”，此时说明防火墙已经被打开了。
	
	3、在命令行中输入systemctl stop firewalld.service命令，进行关闭防火墙。
	
	4、然后再使用命令systemctl status firewalld.service，在下方出现disavtive（dead），这权样就说明防火墙已经关闭。
	
	5、再在命令行中输入命令“systemctl disable firewalld.service”命令，即可永久关闭防火墙。

###docker 运行 rabbitmq
	docker run -d -i -t \
	--name rabbitmq \
	-p 5672:5672 \
	-p 15672:15672 \
	-v rabbitmq-plugins:/plugins \
	-v `pwd`/data:/var/lib/rabbitmq \
	--hostname MasterRabbit \
	-e RABBITMQ_DEFAULT_VHOST=master  \
	-e RABBITMQ_DEFAULT_USER=admin \
	-e RABBITMQ_DEFAULT_PASS=admin \
	rabbitmq:latest

## RabbitMQ
![Alt](https://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/bqQfVz5yrrGYSXMvKr.cqe2HLi4cP7kuksKE5rWRQW*QkYqQB9ihkW4YL3REhCz0CDvHLoxhADHMsmZAtIc1JhCwXECfnHiAdzuQ*yssWL8!/b&bo=KQYoAgAAAAABByU!&rf=viewer_4)

	优点：
	1、服务解耦
	服务间的耦合性越高，容错性就越低，可维护性就越低。使用 MQ 使得服务间解耦，提升容错性和可维护性。
	
	2、任务异步处理
	将不需要同步处理的并且耗时长的操作由消息队列通知消息接收方进行异步处理。提高了轮询服务的响应时间。
	
	3、削峰填谷
	应对大负载，轮询服务高峰期产生的数据会被积压在 MQ中，在高峰期过后的一段时间内，消费消息的速度还是会维持，直到消费完积压的消息,减少高并发引擎服务的承载压力。
	
	
	缺点：
	1、系统可用性降低
	系统引入的外部依赖越多，系统稳定性越差。一旦 MQ 宕机，就会对业务造成影响。如何保证MQ的高可用？
		镜像模式的集群是在普通模式的基础上，通过policy来实现，使用镜像模式可以实现RabbitMQ的高可用方案

	2、系统复杂度提高
	MQ 的加入大大增加了系统的复杂度，现在是通过 MQ 进行异步调用。 如何保证消息没有被重复消费？
		消息重复的原因有两个：1.生产时消息重复，2.消费时消息重复。
	1).生产时消息重复
		保存唯一主键，后续推送的数据，如果存在则过滤掉此数据，如果不存在则插入数据库
	2).消费时消息重复
		
	怎么处理消息丢失情况？
		生产：confirm 发布确认 生产者没有收到确认，实际上MQ已经接收到了消息。这时候生产者就会重新发送一遍这条消息。
		消费：采用手动ack （消息应答机制）
		
	那么保证消息传递的顺序性？
				

	3、一致性问题

###RabbitMQ核心组成部分
####核心概念
	Server：又称Broker，是消息中间件服务的节点，接收客户的连接、实现AMQP实体服务。
	Connection：连接、应用程序与Broker的网络连接，TCP/IP三次握手四次挥手，一个连接中包含成百上千个Channel
	Channel：信道，几乎所有的操作都是在Channel中进行的，Channel提供消息读写的通道，每个Channel代表一个会话任务。信道是建立在TCP连接上的虚拟连接，rabbitmq在一条TCP上建立多个信道来达到多个线程处理，这一条TCP由多个线程共享，每一个线程对应TCP上的一个Channel，它们彼此之间互不影响。
	Message：消息，服务与应用程序之间传送的数据。由Properties和Body组成，Properties可以对消息进行修饰，比如消息的优先级、延迟等高级特性，Body是消息的内容。
	Virtual Host：虚拟消息服务器，每个Virtual Host相当于一个相对独立的RabbitMQ服务器；每个Virtual Host之间是相互隔离的，exchange、queue、message不能互通。可以将RabbitMQ理解为一个数据库，而Virtual Host就是其中的一个库。
	Exchange：交换机，接收消息，根据路由key发送消息到该路由key绑定的消息队列（不具备消息存储的能力），负责投递消息给队列，如果没有 Queue bind 到 Exchange 的话，它会直接丢弃掉 Producer 发送过来的消息。常用的交换机类型有：direct、fanout、topic、headers
	Binding：Exchange交换机和Queue队列之间的虚拟连接。binding中可以保护多个路由key
	Routing key：路由键是一个路由规则，虚拟机会根据路由键路将一个消息从交换机路由到一个绑定的队列。
	Queue ：队列，保存消息，消费者可以从队列中获取消息。

####RabbitMQ四种类型交换机
	direct(routing key)
	处理路由键。需要将一个队列绑定到交换机上，要求该消息与一个特定的路由键完全匹配，这是一个完整的匹配，所谓完整匹配，是指路由键需要一模一样。如果一个队列绑定到该交换机上binding key为 “sms”，则只有发送消息时指定routing key为“sms”的消息才被转发到该队列，不会转发到eamil,也不会转发到sms.abc，只会转发sms。因此，当使用特定 routing key 发送的消息将被传递到与匹配binding key绑定的所有队列。同时，RabbitMQ允许一个队列通过多个binding key与一个交换机进行绑定，在交换机进行消息投递的时候，只要生产者指定的routing key满足其中一个binding key即可将消息路由到指定的队列。如下图，只要生产者发送消息指定routing key为sms或者test，消息都能被投递到Queue2队列。（这里出现的bingding key其实也叫 routing key，只是为了与发送消息时指定的routing key区分开来，避免混淆）
![Alt](https://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/bqQfVz5yrrGYSXMvKr.cqTIP65Yc9J7Xc*a6DItVFi6C5bGI7k2Eb6o0.4GKxV3PpOprzsvR9WEb3Q3Achj7eGOu0*E0LRZhOtbNS2iTemU!/b&bo=5QO3AQAAAAABB3A!&rf=viewer_4)

	fanout类型交换机
	不处理路由键。只需要简单的将队列绑定到交换机上。一个发送到交换机的消息都会被转发到与该交换机绑定的所有队列上。很像子网广播，每台子网内的主机都获得了一份复制的消息。fanout交换机转发消息是最快的。	
![Alt](https://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/bqQfVz5yrrGYSXMvKr.cqUiwIo6Yhf.QTAszESccUkYUSX.tiKbaY9WTCVUqbtRetoyKQYR4eS04jZgJ739cY1.vol19G1S1jsvx4RXloOQ!/b&bo=0AJKAQAAAAABB7k!&rf=viewer_4)

	topic（模糊匹配的routing key）
	topic交换机可以实现更加复杂的消息发送规则，即发送消息时，指定更为复杂的routing key，类似于模糊匹配，routing key可以多变。只要发送消息时指定的routing key符合交换机与队列绑定的binding key的匹配规则，则消息可以被正确投递到指定队列。
	
	模糊匹配符号及其规则
	# ：代表匹配一个多或多个、或者一个也匹配不到,支持多级
	* ：代表必须匹配一个，且只能是一级，即如果binding key为*.sms.*，则只有发送消息时指定routing key为类似 a.sms.b等的消息才会被投递到该队列，如果routing key 为sms.b或者a.sms或者a.b.sms，则都不会被投递到该队列。
![Alt](https://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/bqQfVz5yrrGYSXMvKr.cqRPTu9a7sQ9guo13l*BDGZES1Az0M38q8KdwcCuya2YWIPqfcAjJOpC*R1jkpetmlFsLt1U2CTtizxhZWAgTq.M!/b&bo=PQT9AQAAAAABB.U!&rf=viewer_4)

	headers类型交换机
	headers交换机和topic交换机有点相似，但是topic交换机的路由是基于路由键，而headers交换机的路由则是基于消息的headers数据，所以在发送消息给headers类型的交换机时指定routing key是没有任何效果的。headers类型的交换机在绑定队列时需要指定参数Arguments，发送消息时需要指定headers和Arguments相匹配，消息才能被投递到对应的队列中。

![Alt](https://m.qpic.cn/psc?/V53QLYoX4P3SjB2YFZdU2Xva9P0R06vD/bqQfVz5yrrGYSXMvKr.cqd.AsG3y2XdNMakNAtAH5AS5nGhCWb8g5g.XKdlENTuRhoqYVud*wlp27y58TcwRyfcTyuEVpW4p8ODNLd*buD8!/b&bo=PQS4AQAAAAABB6A!&rf=viewer_4)
