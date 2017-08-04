---
title: "更改 SSIS 的横向扩展日志记录的帐户 |Microsoft 文档"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ec785459e5f9585776d83cde3f460c1e79367e46
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="change-the-account-for-scale-out-logging"></a>更改的帐户向外扩展日志记录。
在向外扩展中执行包，事件消息将记录到 SSISDB 与自动创建用户**# # MS_SSISLogDBWorkerAgentLogin # #**。 此用户的登录使用 SQL Server 身份验证。 若要更改的帐户，如下所示执行以下步骤：

## <a name="1-create-a-user-of-ssisdb"></a>1.创建 SSISDB 的用户
创建数据库用户的说明，请参阅[创建数据库用户](../../relational-databases/security/authentication-access/create-a-database-user.md)。

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2.将用户添加到数据库角色 ssis_cluster_worker

联接数据库角色的说明，请参阅[加入角色](../../relational-databases/security/authentication-access/join-a-role.md)。

## <a name="3-update-logging-information-in-ssisdb"></a>3.更新在 SSISDB 中的日志记录信息
调用存储的过程 [目录]。[update_logdb_info] 使用作为参数的 Sql Server 名称和连接字符串。

#### <a name="example"></a>示例
```tsql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4.重新启动横向扩展辅助服务

> [!NOTE]
> 如果你使用的日志记录的 Windows 用户帐户，则它必须运行缩放出 Worker 服务的相同帐户。 否则，登录到 SQL Server 将失败。
