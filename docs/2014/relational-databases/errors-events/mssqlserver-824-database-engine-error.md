---
title: MSSQLSERVER_824 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 824 (Database Engine error)
ms.assetid: 2aa22246-2712-4fdb-9744-36e7e6f3175e
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0de65488eed3e0e93f706cfba619fe1a5608d328
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407674"
---
# <a name="mssqlserver824"></a>MSSQLSERVER_824
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|824|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|B_HARDSSERR|  
|消息正文|SQL Server 检测到基于一致性的逻辑 I/O 错误: %ls。 在文件 '%ls' 中、偏移量为 %#016I64x 的位置对数据库 ID %d 中的页 %S_PGID 执行 %S_MSG 期间，发生了该错误。  SQL Server 错误日志或系统事件日志中的其他消息可能提供了更详细信息。|  
  
## <a name="explanation"></a>解释  
 此错误表明 Windows 报告已从磁盘成功读取页，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 检测到页中存在错误。 此错误与错误 823 类似，只是 Windows 不检测这一错误。 这通常表明 I/O 子系统中存在问题，例如磁盘驱动器存在故障、磁盘固件存在问题、设备驱动程序不正确等等。 有关 I/O 错误的详细信息，请参阅 [Microsoft SQL Server I/O 基础知识，第 2 章](http://go.microsoft.com/fwlink/?LinkId=69370)。  
  
## <a name="user-action"></a>用户操作  
  
### <a name="look-for-hardware-failure"></a>查找硬件故障  
 运行硬件诊断并更正任何问题。 也可以通过检查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系统和应用程序日志以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志以查看是否存在由硬件故障引起的错误。 修复日志中包含的所有与硬件相关的问题。  
  
 如果持续遇到数据损坏问题，请尝试分别换下不同的硬件组件以确定问题所在。 进行检查以确保系统未启用磁盘控制器上的写缓存。 如果怀疑写入缓存是问题起因，请与硬件供应商联系。  
  
 最后，您可能会发现，切换到全新的硬件系统是解决问题的极佳途径。 此切换操作可能包括重新格式化磁盘驱动器和重新安装操作系统。  
  
### <a name="restore-from-backup"></a>从备份还原  
 如果出现的问题与硬件无关，并且已知的干净备份可用，则请从备份中还原数据库。  
  
 考虑将数据库改为使用 PAGE_VERIFY CHECKSUM 选项。 有关 PAGE_VERIFY 的信息，请参阅 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [管理 suspect_pages 表 (SQL Server)](../backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
