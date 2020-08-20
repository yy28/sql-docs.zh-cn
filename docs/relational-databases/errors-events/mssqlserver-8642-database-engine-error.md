---
description: MSSQLSERVER_8642
title: MSSQLSERVER_8642 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8642 (Database Engine error)
ms.assetid: fc498059-202f-4d0b-8599-4e784b47c186
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ab7d742d6af4b9f2ae29e8cb9cffe645a1d7f49
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460875"
---
# <a name="mssqlserver_8642"></a>MSSQLSERVER_8642
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|8642|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|EXCHNGSTART_ERR|  
|消息正文|查询处理器未能为执行并行查询启动必要的线程资源。|  
  
## <a name="explanation"></a>说明  
服务器中的线程资源不足。  
  
## <a name="user-action"></a>用户操作  
减少服务器上的负载，然后重新运行查询。  
  
