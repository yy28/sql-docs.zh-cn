---
title: CAB 适用于 SQL Server 累积更新的下载 |Microsoft Docs
description: SQL Server 2017 机器学习服务和 SQL Server 2016 R Services 的 CAB 下载。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e1586f94e21304ce994e5e14bf1b4a57ee796a83
ms.sourcegitcommit: fb269accc3786715c78f8b6e2ec38783a6eb63e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2018
ms.locfileid: "43152528"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>实例的 SQL Server 数据库内分析的累积更新 CAB 下载

SQL Server 实例配置为在数据库内分析包括在 CAB 文件中，已安装和维护通过 SQL Server 安装程序提供的 R 和 Python 功能。 

在服务器上连接到 internet，CAB 应用更新，通常通过 Windows 更新。 必须手动更新已断开连接的服务器。 有关脱机安装说明，请参阅[安装 SQL Server 机器学习组件无法访问 internet](sql-ml-component-install-without-internet-access.md)。

本文提供的 SQL Server 2017 机器学习服务 （R 和 Python）-或 SQL Server 2016 R Services-每个累积更新的 CAB 文件的下载链接，以便您可以手动更新与 internet 断开连接的服务器。 

## <a name="prerequisites"></a>必要條件

开始进行基线安装。

+ 在 SQL Server 2017 机器学习服务的初始版本是基线安装。 
+ 在 SQL Server 2016 R Services，您可以开始在初始版本、 SP1 或 SP2。 

接下来，应用[累积更新](https://support.microsoft.com/help/4047329)for SQL Server 数据库引擎实例。

在基准安装并已应用于 SQL Server 累积更新后，可以执行[补充升级](sql-ml-component-install-without-internet-access.md#slipstream-upgrades)安装 CAB 文件与更新机器学习功能。

按时间顺序逆序列出了 CAB 文件。 当您下载 CAB 文件，并将其传输到目标计算机时，将它们放在方便的文件夹等**下载**或安装程序用户的 %temp%文件夹。

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 cab 文件

发行版本  |下载链接  | 已解决的问题 | 
---------|---------------|-------|
**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 无更改。 这是以前的版本。 |
Microsoft R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| 一些小问题修复。|
Microsoft Python 打开     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 无更改。 这是以前的版本。 |
Python 服务器    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| Python rx_data_step 丢失时删除了重复项的行顺序。 <br/>速度失败对聚集列存储索引的数据类型检测。 <br/>当列包含所有 null 值时返回一个空表。 |
**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[cu9 的所有更新](https://support.microsoft.com/help/4341265)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 无更改。 这是以前的版本。 |
Microsoft R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
Microsoft Python 打开     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 无更改。 这是以前的版本。 |
Python 服务器    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 无更改。 这是以前的版本。 |
Microsoft R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
Microsoft Python 打开     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 无更改。 这是以前的版本。 |
Python 服务器    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| SPEES 查询中的日期时间数据类型。<br/>缺少预先训练的模型时，改进了 microsoftml 中的错误消息。<br/> 修补程序，用于 revoscalepy 转换函数和变量。|
**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 无更改。 这是以前的版本。 |
Microsoft R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| RxInstallPackages 中长时间与路径相关的错误。<br/>在环回 RxExec 的连接。
Microsoft Python 打开     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 无更改。 这是以前的版本。 |
Python 服务器    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>在为 rx_exec 环回连接。
**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 无更改。 这是以前的版本。 |
Microsoft R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Microsoft Python 打开     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 无更改。 这是以前的版本。 |
 Python 服务器    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
**[SQL Server 2017 cu3 开始](https://support.microsoft.com/help/4052987)** |  |  |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Microsoft Python 打开     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 无更改。 这是以前的版本。 |
Python 服务器    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| Python 模型 revoscalepy 中的序列化使用[rx_serialize_model 函数](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)。<br/>[本机计分](../sql-native-scoring.md)支持，以及增强功能[实时评分](../real-time-scoring.md)。 
**SQL Server 2017 [CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |
Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| 无更改。 这是以前的版本。 |
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Microsoft Python 打开     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 无更改。 这是以前的版本。 
Python 服务器    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | 将添加 rx_create_col_info 用于返回架构信息。 <br/>增强功能[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)以支持使用的并行方案`RxLocalParallel`计算上下文。|
**初始版本** |  |  |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python 打开     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Python 服务器    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |


<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 cab 文件

SQL Server 2016 R Services 的基线版本是 RTM 版本或 service pack 版本。

发行版本  |下载链接  |
---------|---------------|
**SQL Server 2016 SP2 CU1 CU2**     |
Microsoft R Open     |[SRO_3.2.2.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039)|
Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
**SQL Server 2016 SP1 CU4 CU10**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP1 CU1 CU3**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 CU4 CU9**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU2 CU3**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)

> [!NOTE]
> 
> 当脱机安装 SQL Server 2016 SP1 CU4 或 SP1 CU5，下载 SRO_3.2.2.16000_1033.cab。 如果在安装程序对话框中所示，可以从 FWLINK 831785 下载 SRO_3.2.2.13000_1033.cab，重命名文件为 SRO_3.2.2.16000_1033.cab 然后再安装累积更新。

如果你想要查看适用于 Microsoft R 的源代码，它是可供下载存档.tar 格式为：[下载 R Server 安装程序](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

# <a name="see-also"></a>另请参阅

[安装 SQL Server 机器学习组件没有 internet 访问权限](sql-ml-component-install-without-internet-access.md)
