---
description: MSSQLSERVER_12301
title: MSSQLSERVER_12301 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 12301 (Database Engine error)
ms.assetid: 69455df4-4ce9-4a6f-af5a-8bbc93e21245
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bc924f153aad50b8817b818de18783f4b6cf6b55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88336053"
---
# <a name="mssqlserver_12301"></a>MSSQLSERVER_12301
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|12301|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_UNSUPPORTED_NULLABLE_COLUMNS|  
|消息正文|“*construct*”不支持索引键中具有可以为 Null 的列。|  
  
## <a name="user-action"></a>用户操作  
请勿在索引键中使用可以为 Null 的列。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
