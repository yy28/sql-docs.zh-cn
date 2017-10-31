---
title: "@@SERVICENAME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@SERVICENAME_TSQL'
- '@@SERVICENAME'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVICENAME function'
- names [SQL Server], registry keys
- registry keys [SQL Server]
ms.assetid: 5b0b35be-50ae-411d-a607-bf7464b73624
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: d800a7dc222b3ac25777cd83964b755185817a7a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40servicename-transact-sql"></a>& #x 40; 和 #x 40;SERVICENAME (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在其下运行的注册表项的名称。 @@SERVICENAME返回 MSSQLSERVER，如果当前实例是默认实例; 如果当前实例是命名的实例，此函数将返回的实例名称。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@SERVICENAME  
```  
  
## <a name="return-types"></a>返回类型  
 **nvarchar**  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作为名为 MSSQLServer 的服务运行。  
  
## <a name="examples"></a>示例  
 下面的示例显示了使用 `@@SERVICENAME`。  
  
```  
SELECT @@SERVICENAME AS 'Service Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Service Name                    
------------------------------  
MSSQLSERVER                     
```  
  
## <a name="see-also"></a>另请参阅  
 [配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [管理数据库引擎服务](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  

