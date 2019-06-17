---
title: MSSQLSERVER_7907 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7907 (Database Engine error)
ms.assetid: a1c94e4a-7e91-46e0-9fac-07bbbf6dd018
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0f2b9006c03ec0d22ab9194c385d95a2829c023e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62762406"
---
# <a name="mssqlserver7907"></a>MSSQLSERVER_7907
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7907|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_FS_INVALID_COLUMN_DIRECTORY|  
|消息正文|表错误：分区 ID PN_ID 中的目录 'DIRECTORY' 不是有效的 Filestream 目录。|  
  
## <a name="explanation"></a>解释  
 列目录的名称是分区的关系引擎列 ID。 如果无法将列目录名称转换为列 ID，则该目录不是有效的列目录。  
  
## <a name="user-action"></a>用户操作  
  
### <a name="look-for-hardware-failure"></a>查找硬件故障  
 运行硬件诊断并更正任何问题。 也可以通过检查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系统和应用程序日志以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志来查看是否存在由硬件故障导致的错误。 修复日志中包含的所有与硬件相关的问题。  
  
 如果持续遇到数据损坏问题，请尝试分别换下不同的硬件组件以确定问题所在。 进行检查以确保系统未启用磁盘控制器上的写缓存。 如果怀疑写入缓存是问题起因，请与硬件供应商联系。  
  
 最后，您可能会发现，切换到全新的硬件系统是解决问题的极佳途径。 此切换操作可能包括重新格式化磁盘驱动器和重新安装操作系统。  
  
### <a name="restore-from-backup"></a>从备份还原  
 如果出现的问题与硬件无关，并且您确信有可用的干净备份，请从备份中还原数据库。  
  
### <a name="run-dbcc-checkdb"></a>运行 DBCC CHECKDB  
 不适用。 无法修复此错误。 如果无法从备份还原数据库，请与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客户服务与支持部门 (CSS) 联系。  
  
  
