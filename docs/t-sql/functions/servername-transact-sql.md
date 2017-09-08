---
title: "@@SERVERNAME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@SERVERNAME'
- '@@SERVERNAME_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVERNAME function'
- local servers [SQL Server]
ms.assetid: b0ef33fb-954a-4294-b05b-a87c14ce25a3
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 525da30f048b8d6ca405783c98eea6bcb0f55671
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="servername-transact-sql"></a>@@SERVERNAME (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回正在运行的本地服务器的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>返回类型  
 **nvarchar**  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序在安装时将服务器名设置为计算机名。 若要更改服务器的名称，使用**sp_addserver**，然后重新启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 多个实例，并用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已安装，@@SERVERNAME返回以下本地服务器名称的信息，如果未安装程序后更改本地服务器名称。  
  
|实例|服务器信息|  
|--------------|------------------------|  
|默认实例|*servername*|  
|命名实例|*servername*\\*instancename*|  
|故障转移群集实例 - 默认实例|*virtualservername*|  
|故障转移群集实例 - 命名实例|*virtualservername*\\*instancename*|  
  
 尽管 @@SERVERNAME函数和 SERVERPROPERTY 函数的 SERVERNAME 属性可能会返回类似格式的字符串，信息可能会不同。 SERVERNAME 属性自动报告计算机网络名的更改。  
  
 与此相反，@@SERVERNAME不会报告此类更改。 @@SERVERNAME报告对本地服务器名称使用所做的更改**sp_addserver**或**sp_dropserver**存储过程。  
  
## <a name="examples"></a>示例  
 下面的示例显示了使用 `@@SERVERNAME`。  
  
```  
SELECT @@SERVERNAME AS 'Server Name'  
```  
  
 下面是一个结果集示例。  
  
```  
Server Name  
---------------------------------  
ACCTG  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_addserver &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
