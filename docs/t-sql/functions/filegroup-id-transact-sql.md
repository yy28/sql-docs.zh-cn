---
title: FILEGROUP_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEGROUP_ID_TSQL
- FILEGROUP_ID
dev_langs:
- TSQL
helpviewer_keywords:
- FILEGROUP_ID function
- identification numbers [SQL Server], filegroups
- filegroups [SQL Server], IDs
- IDs [SQL Server], filegroups
- names [SQL Server], filegroups
ms.assetid: 852a76d8-9e61-4a31-84ee-c7edb84a061c
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 998a3dad0b974a6084c7624dea09a592473a1d5c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826976"
---
# <a name="filegroup_id-transact-sql"></a>FILEGROUP_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

此函数返回指定文件组名称的文件组标识 (ID) 号。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
FILEGROUP_ID ( 'filegroup_name' )   
```  
  
## <a name="arguments"></a>参数  
filegroup_name  是类型 sysname  的表达式，它表示文件组 ID `FILEGROUP_ID` 将返回的文件组名称。  
  
## <a name="return-types"></a>返回类型  
**int**  
  
## <a name="remarks"></a>备注  
filegroup_name 与 sys.filegroups 目录视图中的 name 列相对应    。  
  
## <a name="examples"></a>示例  
此示例将返回 `PRIMARY` 数据库中名为 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 的文件组的文件组 ID。  
  
```  
SELECT FILEGROUP_ID('PRIMARY') AS [Filegroup ID];  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Filegroup ID  
------------  
1  

(1 row(s) affected)
 ```  
  
## <a name="see-also"></a>另请参阅  
 [FILEGROUP_NAME (Transact-SQL)](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.filegroups (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
