---
title: MSSQLSERVER_7995 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 7995 (Database Engine error)
ms.assetid: af6d6322-3cba-43d8-be97-e6ef15f8c933
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 169684afef0c30018ff39f977d34a957a9c65a92
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver7995"></a>MSSQLSERVER_7995
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7995|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_SYSTEM_CATALOGS_CORRUPT|  
|消息正文|数据库 'DBNAME'：系统目录中存在一致性错误，无法进一步处理 DBCC CHECKNAME。|  
  
## <a name="explanation"></a>解释  
DBCC CHECKDB 进程包含以下三个阶段：  
  
1.  分配检查。 这等效于运行 DBCC CHECKALLOC。  
  
2.  系统表一致性检查。 这等效于对所需系统基表的小列表运行 DBCC CHECKTABLE。  
  
3.  完成数据库一致性检查。  
  
MSSQLEngine_7995 在第 2 阶段中引发，指示 DBCC CHECKDB 找到该命令无法修复的错误或者尚未指定 REPAIR。 DBCC CHECKDB 无法继续执行第 3 阶段，因为相关的系统基表存储数据库中所有对象的元数据，或者系统基表已损坏。  
  
## <a name="user-action"></a>用户操作  
  
### <a name="look-for-hardware-failure"></a>查找硬件故障  
运行硬件诊断并更正任何问题。 也可以通过检查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系统和应用程序日志以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志来查看是否存在由硬件故障导致的错误。 修复日志中包含的所有与硬件相关的问题。  
  
如果持续遇到数据损坏问题，请尝试分别换下不同的硬件组件以确定问题所在。 进行检查以确保系统未启用磁盘控制器上的写缓存。 如果怀疑写入缓存是问题起因，请与硬件供应商联系。  
  
最后，您可能会发现，切换到全新的硬件系统是解决问题的极佳途径。 此切换操作可能包括重新格式化磁盘驱动器和重新安装操作系统。  
  
### <a name="restore-from-backup"></a>从备份还原  
如果出现的问题与硬件无关，并且您确信有可用的干净备份，请从备份中还原数据库。  
  
### <a name="run-dbcc-checkdb"></a>运行 DBCC CHECKDB  
如果不存在干净的可用备份，请运行不带 REPAIR 子句的 DBCC CHECKDB 以确定损坏程度。 建议使用 DBCC CHECKDB 的 REPAIR 子句。 接下来，请运行带适当 REPAIR 子句的 DBCC CHECKDB 修复损坏的数据。  
  
> [!CAUTION]  
> 如果您不确定运行带有 REPAIR 子句的 DBCC CHECKDB 会对数据造成何种影响，请在运行该语句前与您的主要支持提供商联系。  
  
如果运行具有 REPAIR 子句的 DBCC CHECKDB 无法解决存在的问题，请与主要支持提供商联系。  
  
### <a name="results-of-running-repair-options"></a>运行 REPAIR 选项的结果  
检查错误列表以查看 REPAIR 将对每个错误执行的操作。  
  

