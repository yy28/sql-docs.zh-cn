---
description: MSSQLSERVER_617
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f336f8b1d8cc6f20e259715f6396ce1f5e126d43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470919"
---
# <a name="mssqlserver_617"></a>MSSQLSERVER_617
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|617|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|NODESHASH|  
|消息正文|尝试对数据库 ID %d 中的对象 ID %ld 的描述符进行解哈希运算时，在哈希表中没有找到该描述符。 工作表缺少条目。 请重新运行查询。 如果涉及到游标，请关闭游标，然后重新打开。|  
  
## <a name="explanation"></a>说明  
SQL Server 在工作表中找不到特定项。  
  
## <a name="user-action"></a>用户操作  
  
1.  如果涉及到游标，请关闭游标，然后重新打开。  
  
2.  再次运行查询。  
  
