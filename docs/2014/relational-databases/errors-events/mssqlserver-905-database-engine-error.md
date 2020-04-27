---
title: MSSQLSERVER_905 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d9b80e93f3df2cdc5623e6f2b31a94d50cd524d7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62912551"
---
# <a name="mssqlserver_905"></a>MSSQLSERVER_905
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|905|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBSTARTUP_EE_PARTITIONING|  
|消息正文|数据库 '%.*ls' 不能在此版本的 SQL Server 中启动，因为它包含分区函数 '%.\*ls'。 只有 SQL Server Enterprise Edition 支持分区。|  
  
## <a name="explanation"></a>说明  
 该数据库包含一个或多个已分区表或已分区索引。 此版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能使用分区。 因此，该数据库无法正常启动。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各版本中均不提供已分区的表和索引。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅 SQL Server 2014 的各个[版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="user-action"></a>用户操作  
 使用 sp_detach_db 存储过程分离该数据库。 如有需要，请移动文件，然后使用带有 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 选项的 CREATE DATABASE 将该数据库附加到受支持的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的实例。 对所有表禁用分区并删除分区函数。 再次分离数据库，并将数据库重新附加到当前服务器。  
  
  
