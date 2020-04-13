# Light Paper

## Features 

### Concept of Decentralization

The decentralization of Litentry includes following aspects:

* `Decentralization of identity storage`: User data, including identity credential, should be storage in the user's owned devices, instead of the central data server of service provider.

* `Dentralization of idenity authentication`: The devices which 

\section{协议特点}

\subsection{去中心化概念}

Litentry提出的去中心化，包括以下几个方面

\begin{description}
\item [身份信息存储的去中心化]个人身份的凭证，不在储存在中心化的服务器，而是可以储存在个人指定的任何设备上。
\item [身份信息认证的去中心化]每一台验证设备，只要可以定期的和整个区块链网络进行通信，就可以独立的去验证身份信息，甚至是离线进行。
\item [身份信息关系的去中心化]以往，数据和个人的对应关系，需要通过公私钥进行加密和保存在一个中心化的服务器，比如在互联网中，每一个网站的证书都储存在CA中，区块链中，这个信息保存在整个去中心化网络利，成本更低，也更安全。
\item [身份信息来源的去中心化]每一个认证信息的来源，都可以有多个。比如学历的信息，可以学校官方提供，也可以由同学，学院，实习工作的公司等机构来提供，并提供对应真假信息的奖惩机制。
\end{description}


\subsection{网络互通性}

Litentry基于Polkadot\footnote{https://polkadot.network/}网络，得到了Web3基金会的项目支持\footnote{https://medium.com/web3foundation/web3-foundation-grants-wave-3-recipients-6426e77f1230}。Web3 基金会致力于构建web3.0的基础设施\footnote{https://web3.foundation/}，打造一个去中心化的新互联网环境，Litentry的身份认证概念，是web3.0概念中重要的生态组成部分。

\begin{figure}[h]
\centering
\includegraphics[scale=0.5]{interoperation.png}
\caption{区块链网络层级架构}
\label{fig:interoperation}
\end{figure}

如金字塔所示，在网络的顶层是Polkadot协议，他用来连接不同的区块链，像以太坊\footnote{https://www.ethereum.org/}，EOS\footnote{https://eos.io/}，IBM超级账本都可以通过Polkadot来调用Litentry中的各个模块，储存系统中和账号身份相关的状态。比如：在以太坊中需要存储其每一个矿工服务器的拥有者，这个列表可以储存在Litentry中，其他所有的区块链都可以从Litentry中来调用相关信息，并且使用我们提供的一些方便的接口功能。

在金字塔底层是各个具体应用场景的智能合约。他们可以：
\begin{itemize}
\item 直接调用Litentry自身的验证授权的函数
\item 与其他的智能合约进行通信，比如这里有一个健身房的智能合约，和一个共享办公室的智能合约。用户在健身房进行验证时可以去检查用户是否在附近的共享办公室注册，如果符合条件则可以不需要健身房授权即可进入。
\item 通过Litentry实现与其他区块链上智能合约信息的互通。
\end{itemize}

通过以上的层层互通，每层之间信息互享，真正实现了跨链跨平台身份信息的互联。

\subsection{协议要素}

Litentry的协议中，
我们主要包括四个重要的元素：

\begin{description}
\item [D1 拥有权限的人或组织]在整个区块链网络中都有对应的密钥对和公共地址，我们可以理解为传统网络中的账户名与用户。
\item [D2 人的身份或物联网设备的身份]是一个广义的身份概念，不仅包括人的身份，也包括物的身份。每个用户（自然人或组织）可以拥有多个甚至不同的身份，比如在北京市注册的身份，在爱沙尼亚注册的数字公民，在公安部备案的身份等。每个用户也可以同时拥有不同设备的身份，表示对某一台设备的所属权。
\item [D3 授予的权限]是对应的身份授予的，可以证明具有相应能力的权限的一串数据。比如某个人对其特定信息比如年龄临时的读取权利，或者对某个共享设备比如共享3D打印机一段时间的使用权等等。
\item [D4 外部数据]是权限在流转过程中产生的对应的信息，比如在读取年龄信息是产生的验证是否满18岁的请求时间，地点和场景，或者是3D打印机在以上例子中的打印参数，这些都将做为外部数据发送给对应授权身份的人和使用授权的人（双方或多方），也就是仅仅包括这个活动的参与者。
\end{description}

\begin{figure}[h!]
\centering
\includegraphics[scale=0.45]{runtime.png}
\caption{协议示例}
\label{fig:runtime}
\end{figure}

下面我们以门锁为例：某个民宿的老板采用了我们的协议，他就是D1权限的拥有者，在自己的民宿中安装了一个智能门锁，在区块链中注册了对应身份信息D2，也就在整个网络中公示了自己对门锁设备的拥有权。此后通过区块链授权10月1日当天的使用口令D3给了房客A。房客A通过将权限保存在手机app（Litentry Signer）中，当天入住时，门锁验证设备同时检查了房客A的口令D3以及其在区块链网络上的信用记录，确认无误后验证成功，生成住宿的信息D4，这个信息将返还给房东和房客。
通过这种方式可以看出，我们以去中心和安全的方式共享人或IoT设备的身份，整个过程做到完全没有第三方平台的参与。

\subsection{经济模型}

\subsubsection{验证者}
作为整个生态的开启者和建设者，我们需要不同的验证场景的接入。在每一个验证场景中，都需要有验证设备，有时候是手机，更多的场景下是一个IoT设备。他们都需要定期与区块链进行通信，在每一次通信的过程中，就同时起到了维护区块链网络的作用，那么就可以同时获得网络上通证的奖励。那么安装这样一个验证的设备，就可以定期收到token的奖励，这样就可以激励早期的参与者加入Litentry生态。

\subsubsection{信息提供者}
同时为了激励更多的身份信息提供者参与到网络中来，我们对第三方提供的可靠数据信息，比如上面例子提到的教育背景信息，验证成功之后，申请验证者会支付一定的token给信息提供者，因为提供者补全了所缺的信息。这样也会使整个网络的信息提供方越来越大。

\subsubsection{网络提供方}
对于复杂的商业场景来说，就需要建立智能合约，每一次智能合约的执行，都会消耗极少量的gas费用，这个费用就会提供给网络的矿工，来支付给他们维护这个网络的费用。

\subsubsection{Litentry项目本身}
对与Litentry，我们在每一次注册申请身份的时候，以及授权的时候，收取非常少的费用。得益与可编程的区块链网络，这个费用在早期时候用户少的时候非常低，在项目成熟之后可以收取非常少的费用来支持项目的运营。

同时作为一家的技术公司，我们也制作了软件的开发框架，和对应标准化的硬件验证设备。我们会通过技术支持，以及硬件的销售来提高自身的利润。

\subsection{硬件框架}

我们目前的硬件实现了基于树莓派的签名验证。随着5G，IoT硬件和边缘计算的发展，智能硬件未来将成倍的增加。我们硬件大规模采用Litentry协议做了充足的准备。

我们对与基于ARM框架的区块链硬件有着较丰富的经验。我们正在开发
\begin{itemize}
\item 区块链轻客户端验证设备，设备的私钥储存在设备的硬件TEE(可信执行环境)\footnote{https://en.wikipedia.org/wiki/Trusted\_execution\_environment}中，使得设备私钥无法通过任何手段导出，这样得到远高于软件的保护，使得验证设备的安全性大大提高。
\item 基于加密芯片的低功耗电子身份卡，通过接触供电，内置签名模块，使得验证的使用如同信用卡和身份证一样方便，同时通过零知识证明(Zero Knowledge Proof)，解决了信息读取时的泄漏问题。
\item 团队成员有着多年加密资产钱包的开发经验。我们开发了基于iOS和安卓硬件加密的手机软件，采用了目前业内最高的加密方法。
\end{itemize}


\subsection{软件技术}

\begin{figure}[h!]
\centering
\includegraphics[scale=0.5]{design.png}
\caption{软件框架}
\label{fig:architecture}
\end{figure}

整个系统的软件框架主要分为以下几个模块：

\begin{itemize}
\item 区块链runtime代码\footnote{https://github.com/litentry/litentry-runtime}，这里是Litentry的核心逻辑，提供了与不同区块链之间的接口。
\item 前端web交互app\footnote{https://github.com/litentry/litentry-web-app}，采用rust语言开发，直接编译区块链上的客户端文件，不仅提供了更多的功能，也可以极大的方便身份以及数据信息的查询和管理。所有的商业场景都可以使用，也支持对应的定制。
\item 基于Rust语言和GraphQL中台数据查询服务器\footnote{https://github.com/litentry/litentry-juniper-api}，通过定期的向区块链网络查询验证历史信息。并通过大数据来实现数据的存储和提供缓存。向验证设备提供一个快速的数据通道。支持不同平台型号硬件设备的接入。
\item 前端手机端Litentry Signer\footnote{https://github.com/litentry/litentry-signer}，实现了对私钥的业内最高级别的安全存储，是用户随身使用的签名工具，保存了用户已有的权限。也可以根据对应的场景进行定制开发。
\item 我们提供智能合约的开发工具以及不同的商业模板，方便不同的应用场景开发，也将向开发者提供基于多种语言包括Typescript的开发指导。
\end{itemize}


软件上所有代码都可以在我们的github\footnote{https://github.com/litentry}上查询到。
