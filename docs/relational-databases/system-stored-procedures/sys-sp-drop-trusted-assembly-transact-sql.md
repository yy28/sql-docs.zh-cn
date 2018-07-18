---
title: sys.sp_drop_trusted_assembly (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_drop_trusted_assembly_TSQL
- sp_drop_trusted_assembly
- sys.sp_drop_trusted_assembly_TSQL
- sys.sp_drop_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_drop_trusted_assembly
ms.assetid: ''
caps.latest.revision: ''
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 2ffdc0c87a798b23ce25e544b26ea63132495b53
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37971849"
---
# <a name="sysspdroptrustedassembly-transact-sql"></a>sys.sp_drop_trusted_assembly (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

从服务器上的受信任程序集的列表中删除程序集。

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>语法
```  
sp_drop_trusted_assembly 
    [ @hash = ] 'value'
```  

## <a name="arguments"></a>参数

[ @hash =] '*值*  
要从服务器的受信任程序集的列表中删除的程序集 SHA2_512 哈希值。 受信任的程序集可能会加载启用 clr 严格安全性后，即使是无符号的程序集或数据库未标记为可信。

## <a name="remarks"></a>Remarks  

此过程将删除中的程序集[sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)。

## <a name="permissions"></a>权限

要求的成员身份`sysadmin`固定的服务器角色或`CONTROL SERVER`权限。

## <a name="examples"></a>示例  

下面的示例从服务器的受信任程序集的列表中删除的程序集哈希。  

```  
EXEC sp_drop_trusted_assembly 
0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC; 
```  

## <a name="see-also"></a>请参阅  
  [sys.sp_add_trusted_assembly](sys-sp-add-trusted-assembly-transact-sql.md) [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) [DROP ASSEMBLY &#40;TRANSACT-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

