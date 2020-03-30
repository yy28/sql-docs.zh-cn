---
title: MSSQLSERVER_1406 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1406 (Database Engine error)
ms.assetid: 915f97de-9b74-41f8-8bd5-b2d061416718
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4419796b75fbd10ab866cbf78b67fcab0c1e2ca5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68023161"
---
# <a name="mssqlserver_1406"></a>MSSQLSERVER_1406
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1406|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBM_BADSTATEFORFORCESERVICE|  
|消息正文|无法安全地强制执行服务。 请删除数据库镜像并恢复数据库 "%.*ls" 以获得访问权。|  
  
## <a name="explanation"></a>说明  
由于镜像状态不能保证强制服务过程正确进行，所以 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 不能强制服务。  
  
## <a name="user-action"></a>用户操作  
删除数据库镜像。 然后可以恢复该镜像数据库以获得它的访问权。  
  
## <a name="see-also"></a>另请参阅  
[在数据库镜像会话中强制服务 (Transact-SQL)](~/database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)  
[删除数据库镜像 (SQL Server)](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
