---
title: "@@MAX_CONNECTIONS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@MAX_CONNECTIONS'
- '@@MAX_CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- simultaneous connections [SQL Server]
- maximum number of simultaneous user connections
- '@@MAX_CONNECTIONS function'
- connections [SQL Server], simultaneous
- number of simultaneous user connections
ms.assetid: 57eb9f4b-548f-4212-9684-a11d831c4732
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de4460e3f5dbc0ff2aba83f4c3794528f9100a2e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40maxconnections-transact-sql"></a>& #x 40; 和 #x 40;MAX_CONNECTIONS (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例允许同时进行的最大用户连接数。 返回的数值不一定是当前配置的数值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@MAX_CONNECTIONS  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="remarks"></a>注释  
 实际允许的用户连接数还依赖于所安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本以及应用程序和硬件的限制。  
  
 若要重新配置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接数较少，对于使用**sp_configure**。  
  
## <a name="examples"></a>示例  
 以下示例显示如何返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的最大用户连接数。 此示例假定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 没有针对更少的用户连接进行重新配置。  
  
```  
SELECT @@MAX_CONNECTIONS AS 'Max Connections';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Max Connections  
---------------  
32767            
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [配置函数](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [配置 user connections 服务器配置选项](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
  
  
