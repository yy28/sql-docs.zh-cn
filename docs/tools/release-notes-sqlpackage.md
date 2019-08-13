---
title: DacFx 和 SqlPackage 发行说明 | Microsoft Docs
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
ms.openlocfilehash: 590ca8048d45d9832ff53775512f991268843872
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809450"
---
# <a name="release-notes-for-sqlpackageexe"></a>SqlPackage.exe 的发行说明

[下载最新版本](sqlpackage-download.md) 

本文列出了 SqlPackage.exe 的已发布版本提供的功能和修补程序。

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="182-sqlpackage"></a>18.2 sqlpackage

发布日期：&nbsp;2019 年 4 月 15 日  
内部版本：&nbsp;15.0.4384.2 

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 添加了对边缘约束和边缘约束子句的图形表支持。 | &nbsp; |
| 启用了模型验证规则以支持 SQL Server 2016 及更高版本的索引键的 32 个列。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 由于使用的查询提示不受支持，因此修复了对 SQL Server 2016 RTM 数据库进行的反向工程。 | &nbsp; |
| 修复了 create filegroup 语句之前出现的 auto close alter 语句的部署顺序。 | &nbsp; |
| 修复了 ScriptDom 分析回归，其中“URL”字符串被解释为顶级令牌。 | &nbsp; |
| 修复了分析 alter table add index 语句时出现的空引用异常。 | &nbsp; |
| 修复了始终显示为不同的可为空的持久化计算列的架构比较。| &nbsp; |
| &nbsp; | &nbsp; |

## <a name="181-sqlpackage"></a>18.1 sqlpackage

发布日期：2019 年 2 月 1 日  
生成号：15.0.4316.1  
预览版。

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 添加了对 UTF8 排序规则的支持。 | &nbsp; |
| 对索引视图启用了非聚集列存储索引。 | &nbsp; |
| 已移动到 .NET Core 2.2。 | &nbsp; |
| 将内存支持的存储用于在 .NET Core 上进行架构比较。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 修复了性能以使用旧版基数估计器进行反向工程查询。 | &nbsp; |
| 修复了生成脚本时出现的重大架构比较性能问题。 | &nbsp; |
| 修复了架构偏差检测逻辑以忽略特定扩展事件 (xevent) 会话。 | &nbsp; |
| 修复了图形表的导入顺序。 | &nbsp; |
| 修复了导出具有对象权限的外部表的问题。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知问题

此版本包括面向 .NET Core 2.2 的 sqlpackage 跨平台预览版。 sqlpackage 可以在 macOS 和 Linux 上运行。

| 已知问题 | 详细信息 |
| :---------- | :------ |
| 不支持生成和部署参与者。 | &nbsp; |
| 不支持使用 json 数据序列化的较旧 .dacpac 和 .bacpac 文件。 | &nbsp; |
| 由于区分大小写的文件系统出现问题，因此可能无法解析引用的 .dacpacs（例如 master.dacpac）。 | 一种解决方法是大写引用文件的名称（例如 MASTER.BACPAC）。 |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

发布日期：&nbsp;2018 年 10 月 24 日  
生成号：15.0.4200.1

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 添加了对数据库兼容级别 150 的支持。 | &nbsp; |
| 添加了对托管实例的支持。 | &nbsp; |
| 添加了 MaxParallelism 命令行参数以指定数据库操作的并行度。 | &nbsp; |
| 添加了 AccessToken 命令行参数以在连接到 SQL Server 时指定身份验证令牌。 | &nbsp; |
| 添加了对流式传输 BLOB/CLOB 数据类型以进行导入的支持。 | &nbsp; |
| 添加了对标量 UDF“INLINE”选项的支持。 | &nbsp; |
| 添加了对图形表“MERGE”语法的支持。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 修复了图形表的未解析伪列。 | &nbsp; |
| 修复了使用内存优化表时创建具有内存优化文件组的数据库的问题。 | &nbsp; |
| 修复了将扩展属性包括在外部表中的问题。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

发布日期：2018 年 6 月 22 日  
生成号：14.0.4079.2

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 改进了连接失败的错误消息，包括 SqlClient 异常消息。 | &nbsp; |
| 支持对单分区索引进行索引压缩以便导入/导出。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 修复了 SQL 2017 及更高版本的 XML 列集的反向工程问题。 | &nbsp; |
| 修复了对 Azure SQL 数据库忽略数据库兼容性级别 140 脚本编写的问题。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

发布日期：&nbsp;2018 年 1 月 25 日  
生成号：14.0.3917.1

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 添加了 ThreadMaxStackSize 命令行参数以分析具有大量嵌套语句的 Transact-SQL。 | &nbsp; |
| 数据库目录排序规则支持。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 将 Azure SQL 数据库 .bacpac 导入到本地实例时，修复了由于此版本的 SQL Server 不支持没有密码的数据库主密钥  而出现的错误。 | &nbsp; |
| 修复了图形表的未解析伪列错误。 | &nbsp; |
| 修复了将 SchemaCompareDataModel 用于 SQL 身份验证来比较架构的问题。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

发布日期：2017 年 12 月 12 日  
生成号：14.0.3881.1

### <a name="features"></a>功能

| 功能 | 详细信息 |
| :------ | :------ |
| 添加了对 SQL 2017+ 和 Azure SQL 数据库上的时态保留策略  的支持。 | &nbsp; |
| 添加了 /DiagnosticsFile:"C:\Temp\sqlpackage.log" 命令行参数以指定用于保存诊断信息的文件路径。 | &nbsp; |
| 添加了 /Diagnostics 命令行参数以将诊断信息记录到控制台。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修复程序

| Fix | 详细信息 |
| :-- | :------ |
| 遇到无法识别的数据库兼容性级别时不会进行阻止。 | 相反，将假定最新的 Azure SQL 数据库或本地平台。 |
| &nbsp; | &nbsp; |
