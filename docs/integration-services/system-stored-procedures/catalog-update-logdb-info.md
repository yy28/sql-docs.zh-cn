---
title: "catalog.update_logdb_info （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a898be08859230ab873fd8e358b892789aaed043
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="catalogupdatelogdbinfo-ssisdb-database"></a>catalog.update_logdb_info （SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

更新[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]缩放出日志记录信息。

## <a name="syntax"></a>语法

```sql
update_logdb_info [@server_name = ] server_name, [@connection_string = ] connection_string
```

## <a name="arguments"></a>参数
[ @server_name =] *server_name*  
 可以用来向外扩展登录 Sql Server。 *Server_name*是**nvarchar**。  

 [ @connection_string =] *connection_string*  
 用于横向扩展日志记录的连接字符串。 *Connection_string*是**nvarchar**。

 ## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  

## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
   
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
 
