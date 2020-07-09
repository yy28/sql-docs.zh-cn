---
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
ms.openlocfilehash: ced4c9b3e690b709be9d8f500ff2656cf6b5e220
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727428"
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
  
