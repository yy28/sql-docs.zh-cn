---
description: MSSQLSERVER_2
title: MSSQLSERVER_2 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "2"
helpviewer_keywords:
- 2 (Database Engine error)
ms.assetid: 567fb571-7cda-4ce8-a702-cdff2df5d419
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5ba226502dc53ead97603c776e6f580fe3dba655
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460959"
---
# <a name="mssqlserver_2"></a>MSSQLSERVER_2
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|2|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|在建立与服务器的连接时出错。  在连接到 SQL Server 时，在默认的设置下 SQL Server 不允许远程连接可能会导致此失败。 （提供程序：命名管道提供程序，错误: 40 - 无法打开到 SQL Server 的连接) (.Net SqlClient 数据提供程序)|  
  
## <a name="explanation"></a>说明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未响应客户端请求，可能是因为尚未启动服务器。  
  
## <a name="user-action"></a>用户操作  
确保已启动服务器。  
  
## <a name="see-also"></a>另请参阅  
[管理数据库引擎服务](~/database-engine/configure-windows/manage-the-database-engine-services.md)  
[配置客户端协议](~/database-engine/configure-windows/configure-client-protocols.md)  
[网络协议和网络库](~/sql-server/install/network-protocols-and-network-libraries.md)  
[客户端网络配置](~/database-engine/configure-windows/client-network-configuration.md)  
[配置客户端协议](~/database-engine/configure-windows/configure-client-protocols.md)  
[启用或禁用服务器网络协议](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
