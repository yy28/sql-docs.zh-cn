---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0891558792174f7813446d5c532758e00b45b2e4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780674"
---
# <a name="mssqlserver_1807"></a>MSSQLSERVER_1807
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|1807|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|CANNOT_EX_LOCK|  
|消息正文|无法获得数据库 '%.*ls' 上的排他锁。 请稍后重试该操作。|  
  
## <a name="explanation"></a>说明  
需要对数据库进行排他访问的操作无法获取它。  
  
## <a name="user-action"></a>用户操作  
断开与该数据库的所有连接，或者稍后重试查询。  
  
