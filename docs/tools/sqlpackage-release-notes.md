---
title: Microsoft DacFx & sqlpackage 发行说明 |Microsoft Docs
description: Microsoft sqlpackage 发行说明
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sqlpackage
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: 7d05ec161b89e548cf529bc82c6d714a1960fb0f
ms.sourcegitcommit: 0dff9dd43e80eee900eb92d25df9ca18397f3485
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37080146"
---
# <a name="sqlpackage-release-notes"></a>sqlpackage 发行说明

[下载最新版本](sqlpackage-download.md)

## <a name="sqlpackage-178"></a>sqlpackage 17.8

发布日期：2018 年 6 月 22 日  
内部版本号：14.0.4079.2  

此版本包括以下修复内容：

- 改进了连接失败，包括 SqlClient 异常消息的错误消息。
- 添加了的 MaxParallelism 命令行参数来指定的数据库操作的并行度。
- 支持对导入/导出的单个分区索引的索引压缩。
- 修复 SQL 2017 和更高版本的 XML 列集的反向工程问题。
- 修复了问题，脚本将数据库兼容级别 140 已忽略为 Azure SQL 数据库。

## <a name="sqlpackage-1741"></a>sqlpackage 17.4.1

发布日期： 2018 年 1 月 25 日  
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

## <a name="sqlpackage-on-macos-and-linux-001-preview"></a>在 macOS 和 Linux 0.0.1 （预览版） 上的 sqlpackage

发布日期：2018 年 5 月 9 日  
内部版本号：15.0.4057.1

此版本包含面向.NET Core 2.0 的 sqlpackage 的跨平台预览版本，并且可以在 macOS 和 Linux 上运行。 

此版本是早期预览版具有以下已知问题：

- /P:CommandTimeout 参数被硬编码为 120。
- 不支持生成和部署参与者。
  - 将移动到 System.ComponentModel.Composition.dll 支持的.NET Core 2.1 后修复。
  - 需要处理区分大小写的路径。
- SQL CLR UDT 类型不受支持，包括 SQL Server CLR UDT 类型： SqlGeography、 SqlGeometry 和 SqlHierarchyId。
- 较旧的.dacpac 和.bacpac 文件，使用 json 数据序列化不受支持。
- 由于使用区分大小写的文件系统的问题可能无法解析引用的.dacpacs (例如 master.dacpac)。
  - 一种解决方法就是利用的名称引用文件 (例如 MASTER。BACPAC)。