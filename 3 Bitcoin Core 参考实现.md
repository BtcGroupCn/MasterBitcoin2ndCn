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

### 3.2.1 选择一个Bitcoin Core版本
By default, the local copy will be synchronized with the most recent code, which might be an unstable or beta version of bitcoin. Before compiling the code, select a specific version by checking out a release tag. This will synchronize the local copy with a specific snapshot of the code repository identified by a keyword tag. Tags are used by the developers to mark specific releases of the code by version number. First, to find the available tags, we use the git tag command:</br>
默认情况下，下载的源代码是最新的代码，这可能是一个不稳定版本或Beta版本。 
在编译代码之前，先获取一个release tag，来选择一个特定的版本。 
这将使本地副本与keyword tag所标识的代码库的特定快照同步。 
开发人员使用tag来用版本号标记代码特定release。 
首先，要找到可用的tags，我们使用git tag命令：

```html
$ git tag
v0.1.5
v0.1.6test1
v0.10.0
...
v0.11.2
v0.11.2rc1
v0.12.0rc1
v0.12.0rc2
...
```

The list of tags shows all the released versions of bitcoin. By convention, release candidates, which are intended for testing, have the suffix "rc." Stable releases that can be run on production systems have no suffix. From the preceding list, select the highest version release, which at the time of writing was v0.15.0. To synchronize the local code with this version, use the git checkout command:</br>
tag列表显示所有的发布版本。
根据惯例，用于测试的发布版本有后缀“rc”。
可以在生产系统上运行的稳定版本没有后缀。 
从上面的列表中，选择最高版本的版本，在本书写作时是v0.15.0。
为了使本地代码与此版本同步，使用git checkout命令：

```html
$ git checkout v0.15.0
HEAD is now at 3751912... Merge #11295: doc: Old fee_estimates.dat are discarded by 0.15.0
```

You can confirm you have the desired version "checked out" by issuing the command git status:</br>
使用git status命令，可以确认你有了所需的版本。

```html
$ git status
HEAD detached at v0.15.0
nothing to commit, working directory clean
```

### 3.2.2 配置Bitcoin Core Build
The source code includes documentation, which can be found in a number of files. Review the main documentation located in README.md in the bitcoin directory by typing **more README.md** at the prompt and using the spacebar to progress to the next page. In this chapter, we will build the command-line bitcoin client, also known as bitcoind on Linux. Review the instructions for compiling the bitcoind command-line client on your platform by typing **more doc/build-unix.md**. Alternative instructions for macOS and Windows can be found in the doc directory, as build-osx.md or build-windows.md, respectively.</br>
源代码中包括文档，可以在多个文件中找到。
主文档是bitcoin目录中的README.md。
在本章中，我们将构建命令行比特币客户端，在Linux也称为bitcoind。
查看编译bitcoind命令行客户端的说明，方法是输入：more doc/build-unix.md。
可以在doc目录中找到macOS和Windows的构建说明，分别为build-osx.md或build-windows.md。

Carefully review the build prerequisites, which are in the first part of the build documentation. These are libraries that must be present on your system before you can begin to compile bitcoin. If these prerequisites are missing, the build process will fail with an error. If this happens because you missed a prerequisite, you can install it and then resume the build process from where you left off. Assuming the prerequisites are installed, you start the build process by generating a set of build scripts using the autogen.sh script.</br>
仔细查看构建的前提条件，这些前提在构建文档的第一部分。
这些是在你开始编译比特币之前必须存在于系统上的库。
如果缺少这些条件，构建过程会失败，并提示错误。
如果失败是因为您缺失条件，可以安装它，然后恢复构建过程。
假设要求的库都已经安装了，可以通过使用autogen.sh脚本生成一组构建脚本来启动构建过程。

```html
$ ./autogen.sh
...
glibtoolize: copying file 'build-aux/m4/libtool.m4'
glibtoolize: copying file 'build-aux/m4/ltoptions.m4'
glibtoolize: copying file 'build-aux/m4/ltsugar.m4'
glibtoolize: copying file 'build-aux/m4/ltversion.m4'
...
configure.ac:10: installing 'build-aux/compile'
configure.ac:5: installing 'build-aux/config.guess'
configure.ac:5: installing 'build-aux/config.sub'
configure.ac:9: installing 'build-aux/install-sh'
configure.ac:9: installing 'build-aux/missing'
Makefile.am: installing 'build-aux/depcomp'
...
```

The autogen.sh script creates a set of automatic configuration scripts that will interrogate your system to discover the correct settings and ensure you have all the necessary libraries to compile the code. The most important of these is the configure script that offers a number of different options to customize the build process. Type "./configure --help" to see the various options:</br>
autogen.sh脚本创建一组自动配置脚本，它会询问系统以发现正确的设置，并确保你有编译代码所需的所有库。
其中最重要的是configure脚本，它提供了许多不同的选项来定制构建过程。
输入“./configure --help”查看各种选项。

```html
$ ./configure --help
`configure' configures Bitcoin Core 0.15.0 to adapt to many kinds of systems.

Usage: ./configure [OPTION]... [VAR=VALUE]...

...
Optional Features:
  --disable-option-checking  ignore unrecognized --enable/--with options
  --disable-FEATURE       do not include FEATURE (same as --enable-FEATURE=no)
  --enable-FEATURE[=ARG]  include FEATURE [ARG=yes]

  --enable-wallet         enable wallet (default is yes)

  --with-gui[=no|qt4|qt5|auto]
...
```

The configure script allows you to enable or disable certain features of bitcoind through the use of the --enable-FEATURE and --disable-FEATURE flags, where FEATURE is replaced by the feature name, as listed in the help output. </br>
configure脚本允许你使用--enable-FEATURE和--disable-FEATURE标志来启用或禁用bitcoind的某些功能，其中FEATURE由功能名称替换，就像help输出列出的那样。 

In this chapter, we will build the bitcoind client with all the default features. We won’t be using the configuration flags, but you should review them to understand what optional features are part of the client. If you are in an academic setting, computer lab restrictions may require you to install applications in your home directory (e.g., using --prefix=$HOME).</br>
在本章中，我们构建的bitcoind客户端有所有默认功能。 
我们不使用配置标志，但你应该查看它们，以了解客户端提供了哪些可选功能。 
如果你在学校环境，计算机实验室限制可能需要你在主目录中安装应用程序（例如，使用--prefix = $ HOME）。

Here are some useful options that override the default behavior of the configure script:</br>
以下是一些有用的选项，修改了configure脚本的默认行为：

**--prefix=$HOME**
This overrides the default installation location (which is /usr/local/) for the resulting executable. Use $HOME to put everything in your home directory, or a different path.</br>
这将修改生成的可执行文件的默认安装位置，默认是 /usr/local/。 
使用$HOME将所有内容放在主目录中。

**--disable-wallet**
This is used to disable the reference wallet implementation.</br>
用于禁用参考钱包的实现。

**--with-incompatible-bdb**
If you are building a wallet, allow the use of an incompatible version of the Berkeley DB library.</br>
如果你在构建一个钱包，这允许使用不兼容版本的Berkeley DB库。

**--with-gui=no**
Don't build the graphical user interface, which requires the Qt library. This builds server and command-line bitcoin only.</br>
不构建GUI（GUI要要Qt库）。
这只构建服务器和命令行。

Next, run the configure script to automatically discover all the necessary libraries and create a customized build script for your system:</br>
接下来，运行configure脚本来自动发现所有必需的库，并为你的系统创建一个定制的构建脚本。

```html
$ ./configure
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
...
[many pages of configuration tests follow]
...
$
```

If all went well, the configure command will end by creating the customized build scripts that will allow us to compile bitcoind. If there are any missing libraries or errors, the configure command will terminate with an error instead of creating the build scripts. If an error occurs, it is most likely because of a missing or incompatible library. Review the build documentation again and make sure you install the missing prerequisites. Then run configure again and see if that fixes the error.</br>
如果一切顺利，configure命令将会创建定制的构建脚本，可用于编译bitcoind。
如果缺失库或有错误，configure命令将会以错误信息终止。
如果出现了错误，可能是因为缺少库或是有不兼容的库。
重新检查构建文档，确认你已经安装缺少的条件。然后运行configure，看看错误是否解决了。

### 3.2.3 构建Bitcoin Core可执行程序
Next, you will compile the source code, a process that can take up to an hour to complete, depending on the speed of your CPU and available memory. During the compilation process you should see output every few seconds or every few minutes, or an error if something goes wrong. If an error occurs, or the compilation process is interrupted, it can be resumed any time by typing make again. Type "make" to start compiling the executable application:</br>
下一步，你将编译源代码，这个过程一般可能需要1个小时完成。
在编译的过程中，你应该经常看一下输出结果。如果出现了问题，会显示错误。
如果发生了错误，编译过程会中断，可以输入make来恢复执行。
输入make，开始编译这个可执行应用程序。

```html
$ make
Making all in src
  CXX      crypto/libbitcoinconsensus_la-hmac_sha512.lo
  CXX      crypto/libbitcoinconsensus_la-ripemd160.lo
  CXX      crypto/libbitcoinconsensus_la-sha1.lo
  CXX      crypto/libbitcoinconsensus_la-sha256.lo
  CXX      crypto/libbitcoinconsensus_la-sha512.lo
  CXX      libbitcoinconsensus_la-hash.lo
  CXX      primitives/libbitcoinconsensus_la-transaction.lo
  CXX      libbitcoinconsensus_la-pubkey.lo
  CXX      script/libbitcoinconsensus_la-bitcoinconsensus.lo
  CXX      script/libbitcoinconsensus_la-interpreter.lo

[... many more compilation messages follow ...]

$
```

On a fast system with more than one CPU, you might want to set the number of parallel compile jobs. For instance, make -j 2 will use two cores if they are available. If all goes well, Bitcoin Core is now compiled. You should run the unit test suite with make check to ensure the linked libraries are not broken in obvious ways. The final step is to install the various executables on your system using the make install command. You may be prompted for your user password, because this step requires administrative privileges:</br>
如果系统由多个CPU，可以并行编译。例如使用 make –j2。
如果一切顺利，Bitcoin Core现在已经编译完成。
你应该使用make check来运行单元测试包，以保证链接库没有被破坏。
最后一步是使用make install命令安装各种可执行程序。
可能会提示你输入用户密码，因为这一步需要管理员权限。

```html
$ make check && sudo make install
Password:
Making install in src
 ../build-aux/install-sh -c -d '/usr/local/lib'
libtool: install: /usr/bin/install -c bitcoind /usr/local/bin/bitcoind
libtool: install: /usr/bin/install -c bitcoin-cli /usr/local/bin/bitcoin-cli
libtool: install: /usr/bin/install -c bitcoin-tx /usr/local/bin/bitcoin-tx
...
$
```

The default installation of bitcoind puts it in /usr/local/bin. You can confirm that Bitcoin Core is correctly installed by asking the system for the path of the executables, as follows:</br>
bitcoind 默认的安装位置是/usr/local/bin。
你可以通过询问系统中可执行文件的路径，来确认bitcoin是否安装成功。

```html
$ which bitcoind
/usr/local/bin/bitcoind

$ which bitcoin-cli
/usr/local/bin/bitcoin-cli
```


