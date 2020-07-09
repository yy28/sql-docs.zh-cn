---
title: MSSQLSERVER_17142 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17142 (Database Engine error)
ms.assetid: 83a53507-ac76-4cb9-b116-daf6f42aea1f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dd9f95d863c101b2b8bdc0d502fcafe5773d589f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780858"
---
# <a name="mssqlserver_17142"></a>MSSQLSERVER_17142
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|17142|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|INIT_SRVC_PAUSED|  
|消息正文|SQL Server 服务已经暂停。 不允许进行新的连接。 要恢复此服务，请使用 SQL 计算机管理器或控制面板中的服务应用程序。|  
  
## <a name="explanation"></a>说明  
服务控制管理器暂停了 SQL Server 的服务。  
  
## <a name="user-action"></a>用户操作  
使用 SQL Server 配置管理器恢复 SQL Server 的服务。  
  
