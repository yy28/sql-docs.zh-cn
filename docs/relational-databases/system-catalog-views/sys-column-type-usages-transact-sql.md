---
title: sys. column_type_usages （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_type_usages
- sys.column_type_usages_TSQL
- column_type_usages_TSQL
- sys.column_type_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_type_usages catalog view
ms.assetid: 1ead375e-f662-4837-903f-8947496c51e4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5dc3ff14375d0e07a1235f0ba79ed36e3e084e58
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139989"
---
# <a name="syscolumn_type_usages-transact-sql"></a>sys.column_type_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  具有用户定义类型的每一列在表中对应一行。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|此列所属对象的 ID。|  
|column_id |**int**|列的 ID。 在对象中是唯一的。|  
|**user_type_id**|**int**|用户定义类型的 ID。<br /><br /> 若要返回类型的名称，请在此列上联接到[sys.databases](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目录视图。|  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的标量类型目录视图](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
