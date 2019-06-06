---
title: 限制和已知的问题为 Linux 上的 SSIS |Microsoft Docs
description: 本文介绍的限制和已知的问题的 SQL Server Integration Services (SSIS) 的 Linux 计算机上
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: craigg
ms.date: 06/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: fdf6542f64549233dd5d4ef15dc39a53fefa49a3
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712834"
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>限制和 Linux 上的 SSIS 的已知的问题

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍的限制和已知的问题的 SQL Server Integration Services (SSIS) 在 Linux 上。

## <a name="general-limitations-and-known-issues"></a>常规限制和已知的问题

在此版本的 Linux 上的 SSIS 不支持以下功能：
  - SSIS 目录数据库
  - 由 SQL 代理计划的包执行
  - Windows 身份验证
  - 第三方组件
  - 变更数据捕获 (CDC)
  - SSIS Scale Out
  - 适用于 SSIS 的 azure 功能包
  - Hadoop 和 HDFS 支持
  - Microsoft Connector for SAP BW

其他限制和 Linux 上的 SSIS 的已知的问题，请参阅[发行说明](sql-server-linux-release-notes.md#ssis)。

## <a name="components"></a> 支持和不支持组件

在 Linux 上支持以下内置 Integration Services 组件。 其中一些 Linux 平台上有限制。 此处未列出的内置组件不支持在 Linux 上。

## <a name="supported-control-flow-tasks"></a>支持控制流任务
- 大容量插入任务
- 数据流任务
- 数据事件探查任务
- 执行 SQL 任务
- 执行 T-SQL 语句任务
- 表达式任务
- FTP 任务
- Web 服务任务
- XML 任务

## <a name="control-flow-tasks-supported-with-limitations"></a>支持限制的控制流任务

| 任务 | 限制 |
|------------|---|
| 执行进程任务 | 仅支持进程内模式。 |
| 文件系统任务 | *移动目录*并*设置文件属性*不支持操作。 |
| 脚本任务 | 仅支持标准的.NET Framework Api。 |
| 发送邮件任务 | 仅支持匿名用户模式。 |
| 传输数据库任务 | 不支持 UNC 路径。 |
| | |

## <a name="supported-and-unsupported-maintenance-plan-tasks"></a>支持和不支持维护计划任务

在 SQL Server 维护计划中，通常可以使用各种 SSIS 任务。

在 Linux 上不支持以下维护计划任务：
- 通知操作员
- 执行 SQL Server 代理作业

在 Linux 上支持以下维护计划任务：
- 检查数据库完整性
- 收缩数据库
- 重新组织索引
- 重新生成索引
- 更新统计信息
- 清除历史记录
- 备份数据库
- T-SQL 语句

## <a name="supported-control-flow-containers"></a>支持控制流容器
- 序列容器
- For 循环容器
- Foreach 循环容器

## <a name="supported-data-flow-sources-and-destinations"></a>支持的数据的数据流源和目标
- 原始文件源和目标
- XML 源

## <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>数据流源和目标支持限制

| 组件 | 限制 |
|------------|---|
| ADO.NET 源和目标 | 只支持 SQLClient 数据提供程序。 |
| 平面文件源和目标 | 仅支持 Windows 样式的文件路径，默认路径映射规则应用于的。 例如`D:\home\ssis\travel.csv`变得`/home/ssis/travel.csv`。 |
| OData 源 | 仅支持基本身份验证。 |
| ODBC 源和目标 | 在 Linux 上支持 64 位 Unicode ODBC 驱动程序。 取决于 Linux 上的 UnixODBC 驱动程序管理器。 |
| OLE DB 源和目标 | 仅支持 SQL Server 为 SQL Server Native Client 11.0 和 Microsoft OLE DB 访问接口。 |
| | |

## <a name="supported-data-flow-transformations"></a>支持数据流转换
- Aggregate
- 审核
- 平衡的数据分发服务器
- 字符映射
- 有条件拆分
- 复制列
- 数据转换
- 派生列
- 导出列
- 模糊分组
- 模糊查找
- 导入列
- 查找
- 合并
- 合并联接
- 多播
- 透视
- 行计数
- 渐变维度
- 排序
- 字词查找
- Union All
- 逆透视

## <a name="data-flow-transformations-supported-with-limitations"></a>数据流转换支持限制

| 组件 | 限制 |
|------------|---|
| OLE DB 命令转换 | 与 OLE DB 源和目标相同的限制。 |
| 脚本组件 | 仅支持标准的.NET Framework Api。 |
| | |

## <a name="supported-and-unsupported-log-providers"></a>支持和不支持日志提供程序
内置的 SSIS 日志提供程序支持在 Linux 上除 Windows 事件日志提供程序。

SQL Server 日志提供程序仅支持 SQL 身份验证;它不支持 Windows 身份验证。

用于文本文件、 XML 文件和 SQL Server Profiler 的 SSIS 日志提供程序将其输出写入到指定的文件。 以下注意事项适用于文件路径：
-   如果未提供路径，日志提供程序将写入到主机的当前目录。 如果当前用户没有写入到主机的当前目录的权限，日志提供程序将引发错误。
-   不能在文件路径中使用环境变量。 如果指定的环境变量，您指定的文字文本所示的文件路径。 例如，如果您指定`%TMP%/log.txt`，日志提供程序将追加的文字文本`/%TMP%/log.txt`为当前主机目录。

## <a name="related-content-about-ssis-on-linux"></a>有关在 Linux 上的 SSIS 的相关的内容
-   [提取、 转换和加载使用 SSIS 的 Linux 上的数据](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [使用 ssis conf 配置 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
-   [计划 SQL Server Integration Services 包在 Linux 上的使用 cron 执行](sql-server-linux-schedule-ssis-packages.md)
