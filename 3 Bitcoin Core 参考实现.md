# 3 Bitcoin Core: 参考实现
Bitcoin is an open source project and the source code is available under an open (MIT) license, free to download and use for any purpose. Open source means more than simply free to use. It also means that bitcoin is developed by an open community of volunteers. At first, that community consisted of only Satoshi Nakamoto. By 2016, bitcoin’s source code had more than 400 contributors with about a dozen developers working on the code almost full-time and several dozen more on a part-time basis. Anyone can contribute to the code—including you!</br>
比特币是一个开源项目，源代码根据一个开放（MIT）许可证提供，可免费下载和用于任何目的。
开源不仅仅是自由使用，也意味着比特币是由一个开放的志愿者社区开发的。
最初，这个社区只有中本聪。到了2016年，比特币的源代码有超过400个贡献者，大约十几位开发人员全职工作，几十名开发人员兼职。任何人都可以为代码做贡献！

When bitcoin was created by Satoshi Nakamoto, the software was actually completed before the whitepaper reproduced in [satoshi_whitepaper] was written. Satoshi wanted to make sure it worked before writing about it. That first implementation, then simply known as "Bitcoin" or "Satoshi client," has been heavily modified and improved. It has evolved into what is known as Bitcoin Core, to differentiate it from other compatible implementations. Bitcoin Core is the reference implementation of the bitcoin system, meaning that it is the authoritative reference on how each part of the technology should be implemented. Bitcoin Core implements all aspects of bitcoin, including wallets, a transaction and block validation engine, and a full network node in the peer-to-peer bitcoin network.</br>
当由中本聪创建比特币时，在白皮书发表之前，这个软件实际上已经完成。
中本聪想在白皮书之前确保它能有效工作。
这个第一个实现，称为“比特币Bitcoin”或“Satoshi客户端”，实际上已经被大大修改和改进了。
它已经演变成了Bitcoin Core，以区别于其它兼容的实现。
Bitcoin Core是比特币系统的参考实现，这意味着它权威参考：应该如何实现这个技术的每个部分。Bitcoin Core实现了比特币的所有方面，包括钱包、交易和区块验证引擎，以及在P2P比特币网络中的全网络节点。

Warning：Even though Bitcoin Core includes a reference implementation of a wallet, this is not intended to be used as a production wallet for users or for applications. Application developers are advised to build wallets using modern standards such as BIP-39 and BIP-32 (see [mnemonic_code_words] and [hd_wallets]). BIP stands for Bitcoin Improvement Proposal.</br>
警告：虽然Bitcoin Core包含钱包的参考实现，但并不意味着要用作用户或应用的实际钱包。
建议应用开发人员使用现代标准（如BIP-39和BIP-32）构建钱包。
BIP表示Bitcoin Improvement Proposal（比特币改进提案）。

Bitcoin Core architecture (Source: Eric Lombrozo) shows the architecture of Bitcoin Core.</br>
下图为Bitcoin Core的架构。

![](https://github.com/BtcGroupCn/MasterBitcoin2ndCn/blob/master/images/mbc2_0301.png)</br>
**Figure 1. Bitcoin Core architecture (Source: Eric Lombrozo)**

## 3.1 比特币开发环境
If you’re a developer, you will want to set up a development environment with all the tools, libraries, and support software for writing bitcoin applications. In this highly technical chapter, we’ll walk through that process step-by-step. If the material becomes too dense (and you’re not actually setting up a development environment) feel free to skip to the next chapter, which is less technical.</br>
如果你是开发人员，你要设置一个开发环境，有所有工具、库和支持软件，以便编写比特币应用程序。 
本章涉及的技术细节较多，我们将逐步介绍这个过程。
如果你觉得过于繁琐（并且你实际上并不打算设置开发环境），可以跳到下一章，下一章的技术会浅显一些。

## 3.2 从源码编译Bitcoin Core
Bitcoin Core’s source code can be downloaded as a archive or by cloning the authoritative source repository from GitHub. On the Bitcoin Core download page, select the most recent version and download the compressed archive of the source code, e.g., bitcoin-0.15.0.2.tar.gz. Alternatively, use the git command line to create a local copy of the source code from the GitHub bitcoin page.</br>
Bitcoin Core的源代码可以下载为压缩文件，也可以从GitHub克隆权威的源码库。</br>
- 在Bitcoin Core下载页，选择最近的版本，下载源码的压缩文件，例如bitcoin-0.15.0.2.tar.gz。</br>
https://bitcoincore.org/bin/
-	使用git命令从GitHub bitcoin页面下载源码。</br>
https://github.com/bitcoin/bitcoin

Tip：In many of the examples in this chapter we will be using the operating system’s command-line interface (also known as a "shell"), accessed via a "terminal" application. The shell will display a prompt; you type a command; and the shell responds with some text and a new prompt for your next command. The prompt may look different on your system, but in the following examples it is denoted by a $ symbol. In the examples, when you see text after a $ symbol, don’t type the $ symbol but type the command immediately following it, then press Enter to execute the command. In the examples, the lines below each command are the operating system’s responses to that command. When you see the next $ prefix, you’ll know it’s a new command and you should repeat the process.</br>
提示：在本章的许多例子中，我们使用操作系统的命令行界面（shell），通过terminal应用程序访问。 shell提示你输入命令，并且输出一些文本和一个新的提示，你输入下一个命令。
提示符可能与你的系统上看起来不同，在以下示例中，用$符号表示。
在示例中，不要输入$，而是输入它之后的命令。然后按回车键执行。
在示例中，每个命令下面的行是操作系统对该命令的响应。
当你看到下一个$时，可以输入新的命令，可以一直重复这个过程。

In this example, we are using the git command to create a local copy ("clone") of the source code:</br>
在本例中，我们用git命令把源代码clone到本地。

```html
$ git clone https://github.com/bitcoin/bitcoin.git
Cloning into 'bitcoin'...
remote: Counting objects: 102071, done.
remote: Compressing objects: 100% (10/10), done.
Receiving objects: 100% (102071/102071), 86.38 MiB | 730.00 KiB/s, done.
remote: Total 102071 (delta 4), reused 5 (delta 1), pack-reused 102060
Resolving deltas: 100% (76168/76168), done.
Checking connectivity... done.
$
```

Tip：Git is the most widely used distributed version control system, an essential part of any software developer’s toolkit. You may need to install the git command, or a graphical user interface for git, on your operating system if you do not have it already.
提示：Git是最广泛使用的分布式版本控制系统，是软件开发人员工具包的重要组成部分。
你可能需要在操作系统上安装git命令或图形用户界面。

When the git cloning operation has completed, you will have a complete local copy of the source code repository in the directory bitcoin. Change to this directory by typing **cd bitcoin** at the prompt:
当git克隆操作完成后，将在bitcoin目录中有完整的源代码。 
输入下面命令进入为此目录。

```html
$ cd bitcoin
```





