---
title: MSSQLSERVER_905 | Microsoft Docs
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
- 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: af5da3fbf06dea7712a03152b54bb65001ec2e42
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver905"></a>MSSQLSERVER_905
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|905|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBSTARTUP_EE_PARTITIONING|  
|消息正文|数据库 '%.*ls' 不能在此版本的 SQL Server 中启动，因为它包含分区函数 '%.\*ls'。 只有 SQL Server Enterprise Edition 支持分区。|  
  
## <a name="explanation"></a>解释  
该数据库包含一个或多个已分区表或已分区索引。 此版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能使用分区。 因此，该数据库无法正常启动。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各版本中均不提供已分区的表和索引。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
## <a name="user-action"></a>用户操作  
使用 sp_detach_db 存储过程分离该数据库。 如有需要，请移动文件，然后使用带有 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 选项的 CREATE DATABASE 将该数据库附加到受支持的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的实例。 对所有表禁用分区并删除分区函数。 再次分离数据库，并将数据库重新附加到当前服务器。  
  

