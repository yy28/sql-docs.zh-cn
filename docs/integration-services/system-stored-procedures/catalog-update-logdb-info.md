---
title: catalog.update_logdb_info（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
author: haoqian
ms.author: haoqian
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 4a1717afb32a5763c6fc73a86151b041069b467c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68038604"
---
# <a name="catalogupdate_logdb_info-ssisdb-database"></a>catalog.update_logdb_info（SSISDB 数据库）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

更新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 日志记录信息。

## <a name="syntax"></a>语法

```sql
catalog.update_logdb_info [@server_name = ] server_name, [@connection_string = ] connection_string
```

## <a name="arguments"></a>参数
[ @server_name = ] server_name   
 用于 Scale Out 日志记录的 SQL Server。 server_name 为 nvarchar   。  

 [ @connection_string = ] connection_string   
 用于 Scale Out 日志记录的连接字符串。 connection_string 为 nvarchar   。

 ## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  

## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
   
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
 
