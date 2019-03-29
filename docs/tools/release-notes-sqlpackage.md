---
title: DacFx 和 SqlPackage 发行说明 |Microsoft Docs
description: Microsoft sqlpackage 的发行说明。
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: de45add2b02686f990d68f7c1c23eec385848751
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538773"
---
# <a name="release-notes-for-sqlpackageexe"></a>SqlPackage.exe 的发行说明

[下载最新版本](sqlpackage-download.md)

本文列出了功能和 SqlPackage.exe 的已发布版本提供的修补程序。

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="181-sqlpackage"></a>18.1 sqlpackage

发布日期：2019 年 2 月 1 日  
生成号：15.0.4316.1  
预览版本。

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 添加了的对 UTF8 排序规则。 | &nbsp; |
| 启用索引视图的非聚集列存储索引。 | &nbsp; |
| 移动到.NET Core 2.2。 | &nbsp; |
| 将内存支持存储用于.NET Core 上的架构比较。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 性能修复的旧版基数估计器用于反向工程的查询。 | &nbsp; |
| 修复了重大架构比较性能问题时生成的脚本。 | &nbsp; |
| 修复架构偏差检测逻辑，以便忽略特定的扩展的事件 (xevent) 会话。 | &nbsp; |
| 修复导入图形表排序。 | &nbsp; |
| 修复导出外部表，其中对象的权限。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知问题

此版本包括面向.NET Core 2.2 的跨平台的预览版本的 sqlpackage。 Sqlpackage 可以在 macOS 和 Linux 上运行。

| 已知问题 | 详细信息 |
| :---------- | :------ |
| 不支持生成和部署参与者。 | &nbsp; |
| 较旧的.dacpac 和.bacpac 文件，使用 json 数据序列化不受支持。 | &nbsp; |
| 由于使用区分大小写的文件系统的问题可能无法解析引用的.dacpacs (例如 master.dacpac)。 | 一种解决方法就是利用的名称引用文件 (例如 MASTER。BACPAC)。 |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

发布日期： &nbsp; 2018 年 10 月 24 日  
生成号：15.0.4200.1

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 添加了的对数据库的兼容性级别 150。 | &nbsp; |
| 添加了的对托管实例。 | &nbsp; |
| 添加了的 MaxParallelism 命令行参数来指定的数据库操作的并行度。 | &nbsp; |
| 添加了的 AccessToken 命令行参数，以连接到 SQL Server 时指定的身份验证令牌。 | &nbsp; |
| 添加了对导入流 BLOB/CLOB 数据类型的支持。 | &nbsp; |
| 添加了对标量 UDF 支持 INLINE 选项。 | &nbsp; |
| 添加了的对图形表 'MERGE' 语法。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 图形表的固定无法解析伪列。 | &nbsp; |
| 修复了与内存优化文件组时内存优化表用于创建数据库。 | &nbsp; |
| 修复了包括外部表的扩展的属性。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

发布日期：2018 年 6 月 22 日  
生成号：14.0.4079.2

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 改进了连接失败，包括 SqlClient 异常消息的错误消息。 | &nbsp; |
| 支持对导入/导出的单个分区索引的索引压缩。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 修复 SQL 2017 和更高版本的 XML 列集的反向工程问题。 | &nbsp; |
| 修复了问题，脚本将数据库兼容级别 140 已忽略为 Azure SQL 数据库。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

发布日期： &nbsp; 2018 年 1 月 25 日  
生成号：14.0.3917.1

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 添加了的 ThreadMaxStackSize 命令行参数来分析具有大量嵌套语句的 Transact SQL。 | &nbsp; |
| 数据库目录排序规则支持。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 在导入到的本地实例的 Azure SQL 数据库.bacpac，修复了由于错误_数据库主密钥密码的情况下不支持在此版本的 SQL Server_。 | &nbsp; |
| 修复了在图形表未解析的伪列错误。 | &nbsp; |
| 修复了使用 SQL 身份验证使用 SchemaCompareDataModel 进行比较的架构。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

发布日期：2017 年 12 月 12 日  
生成号：14.0.3881.1

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 添加了对_时态保留策略_SQL 2017 + 和 Azure SQL 数据库上。 | &nbsp; |
| 添加了 /DiagnosticsFile:"C:\Temp\sqlpackage.log"命令行参数来指定文件路径来保存诊断信息。 | &nbsp; |
| 添加了的 /Diagnostics 命令行参数将诊断信息记录到控制台。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 不会阻止时遇到无法识别的数据库兼容级别。 | 相反，因此将假定最新的 Azure SQL 数据库或本地平台。 |
| &nbsp; | &nbsp; |
