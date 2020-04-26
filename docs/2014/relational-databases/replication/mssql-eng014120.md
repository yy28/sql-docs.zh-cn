---
title: MSSQL_ENG014120 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014120 error
ms.assetid: 6b169a3b-30da-4981-b998-b52d61811572
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7472ab39376b84b515ee5b57033a0eda6521ab27
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/25/2020
ms.locfileid: "63191487"
---
# <a name="mssql_eng014120"></a>MSSQL_ENG014120
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14120|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|无法删除分发数据库 '%s'。 此分发服务器数据库与发布服务器相关联。|  
  
## <a name="explanation"></a>说明  
 分发数据库存储事务性复制的所有复制和事务类型的元数据和历史记录数据。 如果试图删除与一个或多个发布服务器相关联的分发数据库，将发生此错误。  
  
## <a name="user-action"></a>用户操作  
 若要删除分发数据库，必须先删除分发服务器与发布服务器之间的关联。 有关详细信息，请参阅 [sp_dropdistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql)。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)   
 [配置分发](configure-distribution.md)  
  
  
