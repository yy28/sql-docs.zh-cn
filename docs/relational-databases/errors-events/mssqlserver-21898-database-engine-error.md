---
title: MSSQLSERVER_21898 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21898 (Database Engine error)
ms.assetid: 02405b21-3d4e-4c2d-b4b3-d7b1ec05edb4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3ba4350b6fc8b9b39833bdf5bdf0c7f7a8613ee7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780494"
---
# <a name="mssqlserver_21898"></a>MSSQLSERVER_21898
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|21898|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21898|  
|消息正文|发布服务器“%s”使用的是分发数据库“%s”，而不是“%s”（后者是承载发布数据库“%s”所需的）。 请在分发服务器“%s”上运行 **sp_changedistpublisher**，以将发布服务器使用的分发数据库更改为“%s”。|  
  
## <a name="explanation"></a>说明  
**sp_validate_redirected_publisher** 在本地分发服务器上查询 msdb.dbo.MSdistpublishers，以验证新的发布服务器使用的分发数据库与原始发布服务器使用的分发数据库相同。 当这些数据库不同时将返回此错误，同时使发布服务器不适合作为发布服务器数据库的主机。  
  
## <a name="user-action"></a>用户操作  
执行存储过程 **sp_changedistpublisher**，以将新发布服务器的分发数据库更改为由原始发布服务器使用的分发数据库。  
  
> [!NOTE]  
> 如果在分发服务器上针对发布服务器运行 **sp_adddistpublisher** 时输入了错误的分发数据库，则运行 **sp_changedistpublisher** 将会解决此问题。 但是，如果远程发布服务器具有其他发布数据库中的现有发布，而这些发布使用所标识的分发数据库，则此更改不适当。 使用命名分发数据库的复制需要系统化地删除，然后使用原始发布服务器的分发数据库重新建立，这样，新的发布服务器才能成为合适的主机。  
  
