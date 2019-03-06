---
title: Microsoft DacFx & sqlpackage 发行说明 |Microsoft Docs
description: Microsoft sqlpackage 发行说明
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: f9fe0558b169acea58bb98a4f9a07267549aa58f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012998"
---
# <a name="sqlpackage-release-notes"></a>sqlpackage 发行说明

[下载最新版本](sqlpackage-download.md)

## <a name="sqlpackage-181"></a>sqlpackage 18.1

发布日期：2019 年 2 月 1 日  
内部版本：15.0.4316.1 

版本包括以下功能和修补程序：

- 添加了的对 UTF8 排序规则。
- 性能修复的旧版基数估计器用于反向工程的查询。
- 启用对索引视图的非聚集列存储索引。
- 修复了重大架构比较性能问题时生成的脚本。
- 修复架构偏差检测逻辑，以便忽略特定 xevent 会话。
- 修复导入图形表排序。
- 修复导出外部表，其中对象的权限。
- 移动到.NET Core 2.2 
- 将内存支持存储用于.NET Core 上的架构比较。

此版本包括跨平台的预览版本的 sqlpackage 面向.NET Core 2.2，并可以在 macOS 和 Linux 上运行。 此预览版本具有以下已知的问题：

- 不支持生成和部署参与者。
- 较旧的.dacpac 和.bacpac 文件，使用 json 数据序列化不受支持。
- 由于使用区分大小写的文件系统的问题可能无法解析引用的.dacpacs (例如 master.dacpac)。
  - 一种解决方法就是利用的名称引用文件 (例如 MASTER。BACPAC)。
## <a name="sqlpackage-180"></a>sqlpackage 18.0

发布日期：2018 年 10 月 24日日  
生成： 15.0.4200.1 

版本包括以下功能和修补程序：

- 添加了的对数据库的兼容性级别 150。
- 添加了的对托管实例。
- 添加了的 MaxParallelism 命令行参数来指定的数据库操作的并行度。
- 添加 AccessToken 命令行参数，以连接到 SQL Server 时指定的身份验证令牌。
- 添加了对导入流 BLOB/CLOB 数据类型的支持。
- 添加了对标量 UDF 支持 INLINE 选项。
- 添加了的对图形表 'MERGE' 语法。
- 图形表的固定无法解析伪列。
- 修复了与内存优化文件组时内存优化表用于创建数据库。
- 修复了包括外部表的扩展的属性。

## <a name="sqlpackage-178"></a>sqlpackage 17.8

发布日期：2018 年 6 月 22 日  
内部版本号：14.0.4079.2  

此版本包括以下修复内容：

- 改进了连接失败，包括 SqlClient 异常消息的错误消息。
- 支持对导入/导出的单个分区索引的索引压缩。
- 修复 SQL 2017 和更高版本的 XML 列集的反向工程问题。
- 修复了问题，脚本将数据库兼容级别 140 已忽略为 Azure SQL 数据库。

## <a name="sqlpackage-1741"></a>sqlpackage 17.4.1

发布日期：2018 年 1 月 25日日  
内部版本号：14.0.3917.1

此版本包括以下修复内容：

- 在导入到的本地实例的 Azure SQL 数据库.bacpac，修复了由于数据库主密钥密码的情况下不支持在此版本的 SQL Server 的错误。
- 数据库目录排序规则支持。
- 修复了在图形表未解析的伪列错误。
- 添加了的 ThreadMaxStackSize 命令行参数来分析具有大量嵌套语句的 TSQL。
- 修复了使用 SQL 身份验证使用 SchemaCompareDataModel 进行比较的架构。

## <a name="sqlpackage-1740"></a>sqlpackage 17.4.0

发布日期：2017 年 12 月 12 日  
内部版本号：14.0.3881.1

此版本包括以下修复内容：

- 不会阻止时遇到数据库兼容性级别不理解。 相反，因此将假定的最新的 Azure SQL 数据库或在本地平台。
- 添加了的对 SQL2017 + 和 Azure SQL 数据库上的临时保留策略。
- 添加了 /DiagnosticsFile:"C:\Temp\sqlpackage.log"命令行参数来指定文件路径来保存诊断信息。
- 添加了的 /Diagnostics 命令行参数将诊断信息记录到控制台。

