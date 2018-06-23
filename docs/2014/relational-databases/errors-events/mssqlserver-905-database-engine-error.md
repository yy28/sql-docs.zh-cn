---
title: MSSQLSERVER_905 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d84961f4903ac6dd0a950ceaa8a8fb9368efcf6d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029248"
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
 该数据库包含一个或多个已分区表或已分区索引。 此版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能使用分区。 因此，该数据库无法正常启动。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各版本中均不提供已分区的表和索引。 有关支持的版本的功能的列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[支持的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="user-action"></a>用户操作  
 使用 sp_detach_db 存储过程分离该数据库。 如有需要，请移动文件，然后使用带有 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 选项的 CREATE DATABASE 将该数据库附加到受支持的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的实例。 对所有表禁用分区并删除分区函数。 再次分离数据库，并将数据库重新附加到当前服务器。  
  
  