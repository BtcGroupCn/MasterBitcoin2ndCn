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
