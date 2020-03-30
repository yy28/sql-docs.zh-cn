---
title: '@@SERVERNAME (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 09a7e9d6199b3227b51cb67a0687c2b812bd21d2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68031586"
---
# <a name="x40x40servername-transact-sql"></a>&#x40;&#x40;SERVERNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回正在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地服务器的名称。  
 ![文章链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>返回类型  
 **nvarchar**  
  
## <a name="remarks"></a>备注  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序在安装时将服务器名设置为计算机名。 若要更改服务器的名称，请使用 **sp_addserver**，然后重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 安装了多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，如果本地服务器名称自安装后未发生更改，则 @@SERVERNAME 返回以下本地服务器名称信息。  
  
|实例|服务器信息|  
|--------------|------------------------|  
|默认实例|'*servername*'|  
|命名实例|'*servername*\\*instancename*'|  
|故障转移群集实例 - 默认实例|'*network_name_for_fci_in_wsfc*'|  
|故障转移群集实例 - 命名实例|'*network_name_for_fci_in_wsfc*\\*instancename*'|  
  
 尽管 @@SERVERNAME 函数和 SERVERPROPERTY 函数的 SERVERNAME 属性可能返回相似格式的字符串，但信息会有所不同。 SERVERNAME 属性自动报告计算机网络名的更改。  
  
 相比之下，@@SERVERNAME 不报告此更改。 @@SERVERNAME 报告使用 **sp_addserver** 或 **sp_dropserver** 存储过程对本地服务器名所做的更改。  
  
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
 [sp_addserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
