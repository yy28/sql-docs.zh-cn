---
title: '@@MAX_CONNECTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0066488fd917e5ffbe88767318954c1727adf238
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68130329"
---
# <a name="x40x40max_connections-transact-sql"></a>&#x40;&#x40;MAX_CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例允许同时进行的最大用户连接数。 返回的数值不一定是当前配置的数值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@MAX_CONNECTIONS  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="remarks"></a>备注  
 实际允许的用户连接数还依赖于所安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本以及应用程序和硬件的限制。  
  
 若要重新配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，以减少允许的连接数，请使用 sp_configure  。  
  
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
  
  
