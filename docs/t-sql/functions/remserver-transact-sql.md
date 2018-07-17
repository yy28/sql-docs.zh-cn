---
title: '@@REMSERVER (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@REMSERVER'
- '@@REMSERVER_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], remote servers
- remote servers [SQL Server], logins
- '@@REMSERVER function'
ms.assetid: 0bb451a9-3866-4064-963d-b74a2f864049
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7b8d3ff79467cd38f8057e121d151c8e765794b1
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37783998"
---
# <a name="x40x40remserver-transact-sql"></a>&#x40;&#x40;REMSERVER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 请改用链接服务器和链接服务器存储过程。  
  
 返回远程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库服务器在登录记录中显示的名称。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@REMSERVER  
```  
  
## <a name="return-types"></a>返回类型  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Remarks  
 使用 @@REMSERVER，存储过程可以检查其运行所在的数据库服务器的名称。  
  
## <a name="examples"></a>示例  
 以下示例将创建返回远程服务器名称的过程 `usp_CheckServer`。  
  
```  
CREATE PROCEDURE usp_CheckServer  
AS  
SELECT @@REMSERVER;  
```  
  
 以下存储过程是在本地服务器 `SEATTLE1` 上创建的。 用户登录到远程服务器 `LONDON2` 上，然后运行 `usp_CheckServer`。  
  
```  
EXEC SEATTLE1...usp_CheckServer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------  
LONDON2  
```  
  
## <a name="see-also"></a>另请参阅  
 [配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [远程服务器](../../database-engine/configure-windows/remote-servers.md)  
  
  
