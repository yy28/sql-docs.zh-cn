---
title: MSSQLSERVER_1461 | Microsoft Docs
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
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 77d6dc184ece81e27083635c9cf049fd079d3e33
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1461"></a>MSSQLSERVER_1461
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1461|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBM_SAFETY_MISMATCH|  
|消息正文|在服务器中检测到数据库"%.*ls"的不同数据库镜像安全级别。 将使用 FULL 安全级别。|  
  
## <a name="explanation"></a>解释  
修改事务安全级别时镜像连接断开，因为事务安全设置在主体数据库和镜像数据库中不一致。 将使用完全事务安全的默认安全设置。 会话将在高安全模式下运行。  
  
## <a name="user-action"></a>用户操作  
若要关闭事务安全，请对主体数据库重新运行 ALTER DATABASE *database_name* SET PARTNER SAFETY OFF 语句。  
  

