---
description: MSSQLSERVER_41302
title: MSSQLSERVER_41302 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41302 (Database Engine error)
ms.assetid: 01e75618-afec-4232-ba68-93ab7bc31003
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 63e32173f062087e0fd912ae0f29292e1fce1e87
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428699"
---
# <a name="mssqlserver_41302"></a>MSSQLSERVER_41302
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41302|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|WRITE_WRITE_CONFLICT|  
|消息正文|当前事务尝试更新自该事务启动后已更新的记录。 该事务已中止。|  
  
## <a name="explanation"></a>说明  
事务遇到写/写冲突，语句已终止。  
  
## <a name="user-action"></a>用户操作  
稍后在其他事务中重试该操作。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
