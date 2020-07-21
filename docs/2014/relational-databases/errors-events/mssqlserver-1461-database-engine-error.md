---
title: MSSQLSERVER_1461 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aaaa21c18a2bf7726b2b8df2e6f2886409cf7ab2
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553792"
---
# <a name="mssqlserver_1461"></a>MSSQLSERVER_1461
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1461|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBM_SAFETY_MISMATCH|  
|消息正文|在服务器中检测到数据库"%.*ls"的不同数据库镜像安全级别。 将使用 FULL 安全级别。|  
  
## <a name="explanation"></a>说明  
 修改事务安全级别时镜像连接断开，因为事务安全设置在主体数据库和镜像数据库中不一致。 将使用完全事务安全的默认安全设置。 会话将在高安全模式下运行。  
  
## <a name="user-action"></a>用户操作  
 若要关闭事务安全，请对主体数据库重新运行 ALTER DATABASE *database_name* SET PARTNER SAFETY OFF 语句。  
  
  
