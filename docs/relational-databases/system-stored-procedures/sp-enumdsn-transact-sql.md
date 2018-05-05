---
title: sp_enumdsn (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 90d5e3c361471777952378cccfafb9f5b4f479fc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spenumdsn-transact-sql"></a>sp_enumdsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对于使用特定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 用户帐户运行的服务器，返回所有定义的 ODBC 和 OLE DB 数据源名称的列表。 此存储过程在发布服务器的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**数据源名称**|**sysname**|数据源的名称。|  
|**Description**|**varchar(255)**|对数据源的说明。|  
|**类型**|**int**|数据源类型：<br /><br /> **1** = ODBC DSN<br /><br /> **3** = OLE DB 数据源|  
|**提供程序名称**|**varchar(255)**|OLE DB 访问接口的名称。 ODBC DSN 的值为 NULL。|  
  
## <a name="remarks"></a>注释  
 每个[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务具有的用户上下文。 用户上下文是一组注册表项，其中包含用户的 ODBC 数据源定义。 用户上下文由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在其下运行的用户名提供。  
  
 例如，如果服务器运行于系统帐户用户上下文中，则返回的数据源名称 (DSN) 将全部是与系统帐户关联的系统 DSN。 如果服务器在专用用户帐户下运行，则只返回为该用户的专用帐户定义的 DSN。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_enumdsn**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_dsninfo &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
