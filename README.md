# Proxy_VPN_SSH
代理、vpn、ssh协议等网络技术及常用命令学习，linux命令查询网站：https://262235.xyz/linux-command/

## 内网ip与外网ip

  以下三种是内网ip，这三种地址是不允许出现在外网上

  A类地址范围：10.0.0.0 ~ 10.255.255.255
  B类地址范围：172.16.0.0 ~ 172.31.255.255
  c类地址范围：192.168.0.0 ~ 192.168.255.255

  内网ip用于局域网之间计算机互相通信，要想和外网，及互连网，则需要借助网关，网关具有内网和外网两个ip地址，通过NAT技术可以实现和外网通信。



## localhost，127.0.0.1 和 主机ip

### localhost

    localhost是一个主机名，指的是调用自身计算机系统，这意味着当我们调用localhost时，机器将与自己对话。

    它帮助我们检查机器中的网络服务，即使在网络硬件故障期间。在使用localhost时，可以通过称为回环Loopback逻辑网络接口访问本地网络服务。Loopback接口的IP地址为127.0.0.1。因此，作为名称     解析的一部分，localhost本地主机解析为127.0.0.1。

    首先 localhost 是一个域名，在过去它指向 127.0.0.1 这个IP地址。在操作系统支持 ipv6 后，它同时还指向ipv6 的地址 [::1] 
    在 Windows 中，这个域名是预定义的，从 hosts 文件中可以看出：

    而在 Linux 中，其定义位于 /etc/hosts 中

### 127.0.0.1

    127.0.0.1 这个地址通常分配给 loopback 接口。loopback 是一个特殊的网络接口(可理解成虚拟网卡)，用于本机中各个应用之间的网络交互。只要操作系统的网络组件是正常的，loopback 就能工     作。Windows 中看不到这个接口，Linux中这个接口叫 lo

    事实上整个 127.* 网段都算能够使用，比如你 ping 127.0.0.2 也是通的。 但是使用127.0.0.1作为loopback接口的默认地址只是一个惯例
  
    整个127.* 网段通常被用作 loopback 网络接口的默认地址，按惯例通常设置为 127.0.0.1。这个地址在其他计算机上不能访问，就算你想访问，访问的也是自己，因为每台带有TCP/IP协议栈的设备基     本上都有 localhost/127.0.0.1

### 本机ip地址

    确切地说，“本机地址”并不是一个规范的名词。通常情况下，指的是“本机物理网卡所绑定的网络协议地址”。通常仅指IP地址甚至ipv4地址。一般情况下，并不会把 127.0.0.1当作本机地址——因为没必     要特别说明，大家都知道。 本机地址是与具体的网络接口绑定的。比如以太网卡、无线网卡或者PPP/PPPoE拨号网络的虚拟网卡，想要正常工作都要绑定一个地址，否则其他设备就不知道如何访问它




## SSH协议及其作用

### 摘自维基百科：

#### 简介：

        Secure Shell（安全外壳协议，简称SSH）是一种加密的网络传输协议，可在不安全的网络中为网络服务提供安全的传输环境。SSH通过在网络中建立安全隧道（secure channel）来实现SSH客户端         与服务器之间的连接。SSH最常见的用途是远程登录系统，人们通常利用SSH来传输命令行界面和远程执行命令。SSH使用频率最高的场合是类Unix系统，但是Windows操作系统也能有限度地使用             SSH。

        在设计上，SSH是Telnet和非安全shell的替代品。Telnet和Berkeley rlogin（rlogin）、rsh、rexec（Remote Process Execution）等协议采用明文传输，使用不可靠的密码，容易遭到监           听、嗅探和中间人攻击。SSH旨在保证非安全网络环境（例如互联网）中信息加密完整可靠。

        不过，SSH也被指出有被嗅探甚至解密的漏洞。早在2011年，中国的网际网路审查机构已经有能力针对SSH连线的刺探及干扰。而后爱德华·斯诺登泄露的文件也指出，美国国家安全局有时能够把SSH         协议传输的信息
        
        解密出来，从而读出SSH会话的传输内容。2017年7月6日，非营利组织维基解密确认美国中央情报局已经开发出能够在Windows或Linux操作系统中窃取SSH会话的工具。

#### 应用：

        SSH的经典用途是登入到远程电脑中执行命令。除此之外，SSH也支持隧道协议、端口映射和X11连接。借助SFTP或SCP协议，SSH还可以传输文件。

        SSH使用客户端-服务器模型，标准端口为22。服务器端需要开启SSH守护进程以便接受远端的连接，而用户需要使用SSH客户端与其建立连接。

        大多数现代操作系统（包括macOS、大部分Linux、OpenBSD、FreeBSD、Solaris等系统）都提供了SSH，包括Windows系统也提供SSH程序（在Windows 10 1809版本之后）。在软件层次，许多关于         SSH的专有软件、免费软体和开源软件被研发出来，如：

        文件管理软件（同步、复制、删除等）。如：PuTTY和Windows下的WinSCP、类Unix系统下的Konqueror等。
        
        从云计算的角度上讲，SSH能够阻止一些因直接暴露在互联网而产生的安全问题，在解决连接问题上发挥了重要作用。SSH隧道可以在互联网、防火墙和虚拟机之间提供一个安全的通道。

#### 历史：

        芬兰赫尔辛基理工大学的塔图·于勒宁发现自己学校存在嗅探密码的网络攻击，便于1995年编写了一套保护信息传输的程序，并称其为“secure shell”，简称SSH[13]，设计目标是取代先前的               rlogin、Telnet、FTP和rsh等安全性不足的协议。1995年7月，于勒宁以免费软体的形式将其发布。程序很快流行起来，截至1995年底，SSH的用户数已经达到两万，遍布五十个国家。

        1995年12月，于勒宁创立了SSH通信安全公司来继续开发和销售SSH。SSH的早期版本用到了很多自由软件，例如GNU libgmp，但后来由SSH公司发布的版本逐渐变成了专有软件。

        1999年，开发者们希望使用自由版本的SSH，于是重新使用较旧的1.2.12版本，这也是最后一个采用开放源代码许可的版本。随后瑞典程序员Björn Grönvall基于这个版本开发了OSSH。不久之后，         OpenBSD的开发者又在Grönvall版本的基础上进行了大量修改，形成了OpenSSH，并于OpenBSD 2.6一起发行。从该版本开始，OpenSSH又逐渐移植到了其他操作系统上面。

        截至2005年，OpenSSH是唯一一种最流行的SSH实现，而且成为了大量操作系统的默认组件，而OSSH已经过时。OpenSSH仍在维护，而且已经支持SSH-2协议。从7.6版开始，OpenSSH不再支持SSH-1         协议

        2006年，SSH-2协议成为了新的标准。与SSH-1相比，SSH-2进行了一系列功能改进并增强了安全性，例如基于迪菲-赫尔曼密钥交换的加密和基于讯息鉴别码的完整性检查。SSH-2还支持通过单个SSH         连接任意数量的shell会话。SSH-2协议与SSH-1不兼容，由于更加流行，一些实现（例如lsh和Dropbear）只支持SSH-2协议。

#### 基本架构：

        SSH协议框架中最主要的部分是三个协议：

        传输层协议（The Transport Layer Protocol）：传输层协议提供服务器认证，数据机密性，信息完整性等的支持。
        用户认证协议（The User Authentication Protocol）：用户认证协议为服务器提供客户端的身份鉴别。
        连接协议（The Connection Protocol）：连接协议将加密的信息隧道复用成若干个逻辑通道，提供给更高层的应用协议使用。
  
        同时还有为许多高层的网络安全应用协议提供扩展的支持。

        各种高层应用协议可以相对地独立于SSH基本体系之外，并依靠这个基本框架，通过连接协议使用SSH的安全机制。

#### 安全验证

        在客户端来看，SSH提供两种级别的安全验证。

        第一种级别（基于密码的安全验证），知道帐号和密码，就可以登录到远程主机，并且所有传输的数据都会被SSH传输层协议加密。但是，可能会有别的服务器在冒充真正的服务器，但只要客户端校         验主机公钥，在服务器私钥不泄露的前提下就能避免被“中间人”攻击。

        第二种级别（基于密钥的安全验证），需要依靠密钥，也就是你必须为自己创建一对密钥，并把公钥放在需要访问的服务器上。客户端软件会向服务器发出请求，请求用你的私钥进行安全验证并发送         使用私钥对会话ID等信息的签名。服务器收到请求之后，先在你在该服务器的用户根目录下寻找你的公钥，然后把它和你发送过来的公钥进行比较，并用公钥检验签名是否正确。如果两个密钥一致，         且签名正确，服务器就认为用户登录成功。

        在服务器端来看，SSH也提供安全验证。

        服务器将自己的公钥分发给相关的客户端，并将密钥交换过程中的公开信息与协商密钥的哈希值的签名发送给客户端，客户端将获取的服务器公钥计算指纹并与其他安全信道获得的公钥指纹相比对并         验证主机签名。

        存在一个密钥认证中心，所有提供服务的主机都将自己的公钥提交给认证中心，公钥认证中心给服务端颁发证书，而任何作为客户端的主机则只要保存一份认证中心的公钥就可以了。在这种模式下，         服务器会发送认证中心提供给主机的证书与主机对密钥交换过程中公开信息的签名。客户端只需要验证证书的有效性并验证签名。

### ssh命令及用途

#### 基本用法：

        ssh -p 22 user@host

        参数：-p 指定端口号  user 登录的用户名  host 登录的主机

        默认端口为22，使用默认端口号时可省

        本地用户名和远程用户名一致可省用户名

#### 远程登录

        首先在终端查看两台机器是否启用ssh

        netstat -ntlp |grep ssh

        使用命令连接

        ssh -p 22 user@host

        输入密码

        成功连接，若想退出，则输入exit

#### 远程操作

        ssh 用户@host 'command'

##### 本地转发

        由本地服务器的某个端口，转发到远程服务器的某个端口，就是把发送到本地端口的请求转发到目标端口，这时访问本地此端口portb相当于访问目标地址hostc的目标端口portc

        ssh -L hostb：portb：hostc：portc 用户@hostc

        本地端口通过跳板映射到其他机器，hosta上启动porta端口，通过hostb转发到hostc的portc上，在hosta上运行。此时访问hosta的porta相当于访问hostc的portc

        ssh -L hosta：porta：hostc：portc 用户@hostb

#### 远程转发

        让远端启动端口，把远端端口的数据传到本地。hosta将自己可以访问的hostb的portb暴露给外网服务器hostc的portc，在hosta上运行，此时相当于hosta让hostb和hostc可以进行通信，hosta起         中间作用

        ssh -R hostc：portc：hostb：portb 用户@hostc

        此时链接hostc的portc就相当于链接hostb的portb。使用时需要修改hostc的/etc/ssh/sshd_config文件，添加 GatewayPorts yes

        此时相当于内网穿透，比如hosta和hostb是同一个内网下的两台可以互相访问的机器，hostc是外网跳板，hostc不能访问hosta，但hosta可以访问hostc。那么通过内网hosta运行此命令，创建           hostc端口监听，把该端口所有数据转发给我hosta，我再转发给hostb，注意hostb和hosta也可以是同一台机器，此时相当于内网hosta把自己可访问的端口暴露给外网hostc访问

#### 本地转发

        本地转发就是把发送到本地的某个端口请求转发到远程的某台机器上面

        ssh -L [本地地址:]本地端口：远程地址：远程端口 远程用户@远程地址

#### 远程转发

        远程转发就是把发给远程机器的某个端口请求，转发到本地的机器上面

        ssh -R [远程地址:]远程端口：本地地址：本地端口 远程用户@远程地址


## ifconfig

    ifconfig用于查看和配置网络接口地址和参数，机器重启后配置就不存在了，想永久修改要修改网卡配置文件。
    


## ip

    ip是iproute2软件包中的强大网络配置工具，它能够替代传统的网络管理工具，如ifconfig和route，使用权限为root，几乎所有的linux发行版都支持这个命令。作用是操控linux主机的路由，
    网络设备、策略路由和隧道。
    
    

















































