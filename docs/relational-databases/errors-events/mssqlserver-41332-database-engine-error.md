---
description: MSSQLSERVER_41332
title: MSSQLSERVER_41332 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1bd040b91e1416dedb6a68317835fe6fcad5b264
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428669"
---
# <a name="mssqlserver_41332"></a>MSSQLSERVER_41332
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41332|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQL_SNAPSHOT_NOT_SUPPORTED|  
|消息正文|当会话 TRANSACTION ISOLATION LEVEL 设置为 SNAPSHOT 时，无法访问或创建内存优化表和本机编译的存储过程。|  
  
## <a name="explanation"></a>说明  
事务在快照隔离级别启动，然后尝试使用不兼容的功能。  
  
## <a name="user-action"></a>用户操作  
使用不同的隔离级别启动事务。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
