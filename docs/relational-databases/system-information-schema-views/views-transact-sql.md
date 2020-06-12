---
title: VIEWS （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- VIEWS_TSQL
- VIEWS
dev_langs:
- TSQL
helpviewer_keywords:
- VIEWS view
- INFORMATION_SCHEMA.VIEWS view
ms.assetid: 6119bc94-0b22-45d4-a34b-967afd810a9d
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a24df8a9c4c85e94259f663b8319d1145a15b565
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670301"
---
# <a name="views-transact-sql"></a>VIEWS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为当前数据库中的当前用户可访问的视图返回一行。  
  
 若要从这些视图中检索信息，请指定 INFORMATION_SCHEMA 的完全限定名称 **。**_view_name_。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar （** 128 **）**|视图限定符。|  
|**TABLE_SCHEMA**|**nvarchar （** 128 **）**|包含该视图的架构名称。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 只是查找对象架构的可靠方法是查询 sys.databases 目录视图。|  
|**TABLE_NAME**|**nvarchar （** 128 **）**|视图名。|  
|**VIEW_DEFINITION**|**nvarchar （** 4000 **）**|如果定义的长度大于**nvarchar （** 4000 **）**，则此列为 NULL。 否则，该列是视图定义文本。|  
|**CHECK_OPTION**|**varchar （** 7 **）**|WITH CHECK OPTION 的类型。 如果最初的视图是使用 WITH CHECK OPTION 创建的，那么就为 CASCADE。 否则，返回 NONE。|  
|**IS_UPDATABLE**|**varchar （** 2 **）**|指定视图是否可更新。 始终返回 NO。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的系统视图 &#40;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [&#40;Transact-sql&#41;的信息架构视图](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.views (Transact-SQL)](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  
