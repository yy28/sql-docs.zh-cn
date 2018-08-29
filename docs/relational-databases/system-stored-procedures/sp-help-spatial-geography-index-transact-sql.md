---
title: sp_help_spatial_geography_index (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_index
- sp_help_spatial_geography_index_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_index procedure
ms.assetid: c9bf5675-eafc-4d71-bfdb-da963384fa0c
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2ec7bb01ce241cb1112a4ca64a0ac26f6d4adf62
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43034098"
---
# <a name="sphelpspatialgeographyindex-transact-sql"></a>sp_help_spatial_geography_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  名称和值的一组指定的属性将返回有关**geography**空间索引。 以表格式返回结果。 可以选择是返回索引的一组核心属性还是返回索引的所有属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_spatial_geography_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput' ]   
     [ , [ @query_sample = ] 'query_sample' ]   
```  
  
## <a name="arguments"></a>参数  
 请参阅[空间索引的参数和属性存储过程](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)。  
  
## <a name="properties"></a>属性  
 请参阅[空间索引的参数和属性存储过程](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)。  
  
## <a name="permissions"></a>Permissions  
 必须为用户分配一个 PUBLIC 角色以便能够访问该过程。 需要服务器和对象的 READ ACCESS 权限。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="example"></a>示例  
 下面的示例使用`sp_help_spatial_geography_index`调查**geography**空间索引**SIndx_SpatialTable_geography_col2**表定义**geography_col**中的给定的查询示例**@qs**。 此示例只返回指定索引的核心属性。  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
exec sp_help_spatial_geography_index 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs;  
```  
  
 边界框**geography**实例是整个地球。  
  
## <a name="requirements"></a>要求  
  
## <a name="see-also"></a>请参阅  
 [空间索引存储过程](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [空间数据 (SQL Server)](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
