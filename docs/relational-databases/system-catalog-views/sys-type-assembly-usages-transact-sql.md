---
description: sys.type_assembly_usages (Transact-SQL)
title: sys. type_assembly_usages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.type_assembly_usages
- sys.type_assembly_usages_TSQL
- type_assembly_usages_TSQL
- type_assembly_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.type_assembly_usages catalog view
ms.assetid: 79b8bf25-6e4e-4a07-ae93-7a4e44f65171
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c6e1bd7aba0b16af1fa59b1064a519f7879207ab
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542416"
---
# <a name="systype_assembly_usages-transact-sql"></a>sys.type_assembly_usages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  每个程序集引用类型在表中各对应一行。  
  

  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**user_type_id**|**int**|类型的 ID<br /><br /> 若要返回类型的名称，请在此列上联接到 [sys.databases](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) 目录视图。|  
|**assembly_id**|**int**|程序集的 ID|  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的标量类型目录视图 ](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
