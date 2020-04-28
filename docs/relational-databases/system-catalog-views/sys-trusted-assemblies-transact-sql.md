---
title: sys. trusted_assemblies （Transact-sql） |Microsoft Docs
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
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9682535c82f8a579259993e82560dfe6bc930f93
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68061365"
---
# <a name="systrusted_assemblies-transact-sql"></a>sys.trusted_assemblies (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

服务器的每个受信任程序集均包含一行。

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|列名称 |数据类型 |说明 |
|--- |--- |--- |
|hash |varbinary(8000) |SHA2_512 程序集内容的哈希。 |
|description |nvarchar(4000) |程序集的可选用户定义说明。 Microsoft 建议使用规范名称对要信任的程序集的简单名称、版本号、区域性、公钥和体系结构进行编码。 此值在公共语言运行时（CLR）端唯一标识程序集，与 sys.databases 中的 clr_name 值相同。 |
|create_date |datetime2 |将程序集添加到受信任程序集列表的日期。 |
|created_by |nvarchar(128) |向列表中添加程序集的主体的登录名。 |
| | | |


## <a name="remarks"></a>备注  

使用 "**需要添加 sp_add_trusted_assembly** ，并**需要添加 trusted_assemblies**添加或删除程序集`sys.trusted_assemblies`。

## <a name="see-also"></a>另请参阅  
  [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [drop assembly &#40;transact-sql&#41;](../../t-sql/statements/drop-assembly-transact-sql.md) sp_add_trusted_assembly  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

