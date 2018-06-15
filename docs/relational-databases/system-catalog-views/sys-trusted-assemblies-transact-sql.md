---
title: sys.trusted_assemblies (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- trusted_assemblies_TSQL
- trusted_assemblies
- sys.trusted_assemblies_TSQL
- sys.trusted_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trusted_assemblies
ms.assetid: ''
caps.latest.revision: ''
author: tmullaney
ms.author: thmullan
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 80fd8a091aa04d0574da5c5a2377628b2e8c376a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33220858"
---
# <a name="systrustedassemblies-transact-sql"></a>sys.trusted_assemblies (TRANSACT-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

包含用于每个服务器的受信任程序集的行。

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|列名 |数据类型 |Description |
|--- |--- |--- |
|哈希 |varbinary （8000) |SHA2_512 哈希值的程序集内容。 |
|description |nvarchar(4000) |程序集的可选用户定义描述。 Microsoft 建议使用将编码简单名称、 版本号、 区域性、 公钥，以及要信任的程序集的体系结构的规范名称。 此值唯一标识一侧公共语言运行时 (CLR) 程序集，并在 sys.assemblies clr_name 值相同。 |
|create_date |datetime2 |程序集添加到受信任的程序集列表的日期。 |
|created_by |nvarchar （128) |程序集添加到列表的主体的登录名。 |
| | | |


## <a name="remarks"></a>注释  

使用**需要添加 sp_add_trusted_assembly**和**需要添加 sys.trusted_assemblies**添加或删除程序集从`sys.trusted_assemblies`。

## <a name="see-also"></a>另请参阅  
  [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys.sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [DROP ASSEMBLY &#40;Transact SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

