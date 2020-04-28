---
title: sys. spatial_reference_systems （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- spatial_reference_systems_TSQL
- sys.spatial_reference_systems_TSQL
- sys.spatial_reference_systems
- spatial_reference_systems
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_reference_systems catalog view
- spatial_reference_systems
ms.assetid: 3c9bc120-67c3-463f-9e24-29fd623f25a0
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e6ffd36516fecba70618c79a7bbd0415f6bb2cb3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68073252"
---
# <a name="sysspatial_reference_systems-transact-sql"></a>sys.spatial_reference_systems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的空间引用系统 (SRID)。  

  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|spatial_reference_id|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的 SRID。|  
|authority_name|**nvarchar(128)**|SRID 的授权。|  
|authorized_spatial_reference_id|**int**|**Authority_name**中名为的机构提供的 SRID。|  
|well_known_text|**nvarchar(4000)**|SRID 的 WKT 表示形式。|  
|unit_of_measure|**nvarchar(128)**|度量单位的名称。|  
|unit_conversion_factor|**float**|以米为度量单位的长度。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
  
