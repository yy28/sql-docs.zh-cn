---
title: sys.trusted_assemblies (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5830d394330778fae6aab795286c7fbc9e211072
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710715"
---
# <a name="systrustedassemblies-transact-sql"></a>sys.trusted_assemblies (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

每个受信任程序集的服务器占一行。

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|列名 |数据类型 |Description |
|--- |--- |--- |
|密切相关的文章 |varbinary(8000) |SHA2_512 哈希值的程序集内容。 |
|description |nvarchar(4000) |程序集的可选用户定义说明。 Microsoft 建议使用简单名称、 版本号、 区域性、 公钥，以及要信任的程序集的体系结构进行编码的规范名称。 此值唯一标识公共语言运行时 (CLR) 端上的程序集，并在 sys.assemblies clr_name 值相同。 |
|create_date |datetime2 |程序集添加到受信任的程序集列表的日期。 |
|created_by |nvarchar （128) |程序集添加到列表的主体的登录名。 |
| | | |


## <a name="remarks"></a>备注  

使用**需要添加 sp_add_trusted_assembly**并**需要添加 sys.trusted_assemblies**添加或删除程序集从`sys.trusted_assemblies`。

## <a name="see-also"></a>请参阅  
  [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys.sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [DROP ASSEMBLY &#40;TRANSACT-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

