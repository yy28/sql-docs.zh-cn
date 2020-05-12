---
title: '@@CONNECTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@CONNECTIONS'
- '@@CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CONNECTIONS function'
- connections [SQL Server], number of
- connections [SQL Server], attempted
- number of connection attempts
- attempted connections
ms.assetid: c59836a8-443c-4b9a-8b96-8863ada97ac7
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 3c7a4a11e3f77316d0f219c4733e3d16fd93ffbc
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827070"
---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

此函数返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自上次启动以来尝试的连接数，无论连接是成功还是失败。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>返回类型
**integer**
  
## <a name="remarks"></a>备注  
连接与用户不同。 应用程序可以打开多个与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接，而不需要用户观察这些连接。
  
为包含几个  **统计信息的报表运行“sp_monitor”** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，包括试图连接统计信息。
  
@@MAX_CONNECTIONS 是允许同时连接到服务器的最大连接数。 @@CONNECTIONS 随每次登录尝试而增加，因此 @@CONNECTIONS 可以超过 @@MAX_CONNECTIONS。
  
## <a name="examples"></a>示例  
此示例返回截至当前日期和时间的登录尝试次数。
  
```sql
SELECT GETDATE() AS 'Today''s Date and Time',   
@@CONNECTIONS AS 'Login Attempts';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
Today's Date and Time  Login Attempts  
---------------------- --------------  
12/5/2006 10:32:45 AM  211023         
```  
  
## <a name="see-also"></a>另请参阅
[系统统计函数 (Transact-SQL)](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)
  
  
