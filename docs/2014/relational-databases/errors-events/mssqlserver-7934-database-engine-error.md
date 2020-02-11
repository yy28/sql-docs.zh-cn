---
title: MSSQLSERVER_7934 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7934 (Database Engine error)
ms.assetid: f656bf46-e5be-4c7b-9ea4-0f2eee7441fe
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1306c4463544d2aee882645a2f0a9401a8fb3a60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62913169"
---
# <a name="mssqlserver_7934"></a>MSSQLSERVER_7934
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7934|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_FS_MISSING_ROWSET_DIRECTORY|  
|消息正文|表错误: 找不到对象 ID O_ID，索引 ID I_ID，分区 ID PN_ID 的 Filestream 目录 ID F_ID。|  
  
## <a name="explanation"></a>说明  
 在运行 DBCC CHECKDB 期间，找到一个分区；但在 FILESTREAM 数据空间中却找不到与其对应的 FILESTREAM 行集目录。  
  
## <a name="user-action"></a>用户操作  
  
### <a name="look-for-hardware-failure"></a>查找硬件故障  
 运行硬件诊断并更正任何问题。 也可以通过检查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系统和应用程序日志以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志来查看是否存在由硬件故障导致的错误。 修复日志中包含的所有与硬件相关的问题。  
  
 如果持续遇到数据损坏问题，请尝试分别换下不同的硬件组件以确定问题所在。 进行检查以确保系统未启用磁盘控制器上的写缓存。 如果怀疑写入缓存是问题起因，请与硬件供应商联系。  
  
 最后，您可能会发现，切换到全新的硬件系统是解决问题的极佳途径。 此切换操作可能包括重新格式化磁盘驱动器和重新安装操作系统。  
  
### <a name="restore-from-backup"></a>从备份还原  
 如果出现的问题与硬件无关，并且您确信有可用的干净备份，请从备份中还原数据库。  
  
### <a name="run-dbcc-checkdb"></a>运行 DBCC CHECKDB  
 不适用。 此错误无法自动修复。 如果无法从备份还原数据库，请与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客户服务与支持部门 (CSS) 联系。  
  
## <a name="see-also"></a>另请参阅  
 [DBCC CHECKDB (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
