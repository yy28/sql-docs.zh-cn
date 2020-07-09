---
title: MSSQLSERVER_41365 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41365 (Database Engine error)
ms.assetid: 4fc7ec15-b722-4e3d-b7f9-3d39d171e96e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 841ea749faa87d66216754ce3aabb61c03d6f996
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765313"
---
# <a name="mssqlserver_41365"></a>MSSQLSERVER_41365
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41365|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_MERGE_SCHEDULE_ERROR|  
|消息正文|未计划数据库 %.*ls 事务范围 [%ld，%ld] 的合并要求。 表示范围的检查点文件对合并不可用或是正在进行的合并的一部分。|  
  
## <a name="explanation"></a>说明  
表示范围的检查点文件对合并不可用或是正在进行的合并的一部分。  
  
## <a name="user-action"></a>用户操作  
为合并提供更好的事务范围/等待，然后再次发出同一请求。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
