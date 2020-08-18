---
description: MSSQLSERVER_10539
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9f1f36f5b8721a94b7badb3316f30f9b3d4e059d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338203"
---
# <a name="mssqlserver_10539"></a>MSSQLSERVER_10539
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|10539|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_NO_PLAN_FOR_STMT|  
|消息正文|由于查询计划对于初始偏移量为 %d 的语句不可用，因此无法从缓存创建计划指南 '%.*ls'。 如果该语句依赖于尚未创建的数据库对象，则可能出现此问题。 请确保所有必要的数据库对象都已存在，并在创建该计划指南之前先执行该语句。|  
  
## <a name="explanation"></a>说明  
在计划缓存中，查询计划不能用于具有指定初始偏移量的语句。  
  
## <a name="user-action"></a>用户操作  
请确保所有必要的数据库对象都已存在，并在创建该计划指南之前先执行该语句。  
  
## <a name="see-also"></a>另请参阅  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
