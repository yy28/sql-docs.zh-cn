---
title: MSSQLSERVER_5243 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5243 (Database Engine error)
ms.assetid: e04a1934-e57d-420e-ac79-97071745824e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 19fd1351963a578d83e8cf67a48c6f97dcd96afe
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68078862"
---
# <a name="mssqlserver_5243"></a>MSSQLSERVER_5243
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5243|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|在内部操作期间检测到不一致性。 请与技术支持联系。 参考号为 %ld。|  
  
## <a name="explanation"></a>说明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 检测到内存的存储引擎结构中存在结构性不一致。  
  
## <a name="user-action"></a>用户操作  
查找硬件故障 运行硬件诊断并更正任何问题。 也可以通过检查 Windows 系统和应用程序日志以及 SQL Server 错误日志以查看是否存在由硬件故障导致的错误发生。 修复日志中包含的所有与硬件相关的问题。

如果持续遇到数据损坏问题，请尝试分别换下不同的硬件组件以确定问题所在。 检查以确保系统未在磁盘控制器上启用写入缓存。 如果怀疑写入缓存是问题起因，请与硬件供应商联系。

最后，您可能会发现，切换到全新的硬件系统是解决问题的极佳途径。 此切换操作可能包括重新格式化磁盘驱动器和重新安装操作系统。

从备份还原 - 如果出现的问题与硬件无关，并且有已知的干净备份可用，请从备份还原数据库。

运行 DBCC CHECKDB - 如果没有干净的备份可用，请运行没有 REPAIR 子句的 DBCC CHECKDB 以确定损坏范围。 建议使用 DBCC CHECKDB 的 REPAIR 子句。 接下来，请运行带适当 REPAIR 子句的 DBCC CHECKDB 修复损坏的数据。

> **不支持警报标记!!!!** 
> **不支持 tr 标记!!!!** 
> **不支持 tr 标记!!!!**

如果运行具有 REPAIR 子句的 DBCC CHECKDB 无法解决存在的问题，请与主要支持提供商联系。
  
## <a name="see-also"></a>另请参阅  
[DBCC CHECKDB (Transact-SQL)](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[数据库文件和文件组](~/relational-databases/databases/database-files-and-filegroups.md)  
  
