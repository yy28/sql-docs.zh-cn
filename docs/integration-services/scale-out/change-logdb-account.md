---
title: "更改 SSIS Scale Out 日志记录的帐户 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dcedbe0d2c2ef2c2089af1e2a8b31fbeb75ce2fc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="change-the-account-for-scale-out-logging"></a>更改 Scale Out 日志记录的帐户
在 Scale Out 中执行包时，会使用自动创建的用户 ##MS_SSISLogDBWorkerAgentLogin## 将事件消息记录到 SSISDB 中。 此用户使用 SQL Server 身份验证登录。 要更改帐户，请执行以下步骤：

## <a name="1-create-a-user-of-ssisdb"></a>1.创建 SSISDB 用户
有关创建数据库用户的说明，请参阅[创建数据库用户](../../relational-databases/security/authentication-access/create-a-database-user.md)。

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2.向数据库角色 ssis_cluster_worker 添加用户

有关加入数据库角色的说明，请参阅[加入角色](../../relational-databases/security/authentication-access/join-a-role.md)。

## <a name="3-update-logging-information-in-ssisdb"></a>3.在 SSISDB 中更新日志记录信息
调用存储过程 [catalog].[update_logdb_info]，并使用 SQL 服务器名称和连接字符串作为参数。

#### <a name="example"></a>示例
```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4.重启 Scale Out Worker 服务

> [!NOTE]
> 如果使用 Windows 用户帐户进行日志记录，该帐户须为运行 Scale Out Worker 服务的帐户。 否则，SQL Server 登录将失败。
