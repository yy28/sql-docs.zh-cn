---
title: sys. sp_drop_trusted_assembly （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50385161b417d02db2dc44ad1172910d31f198b3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905139"
---
# <a name="syssp_drop_trusted_assembly-transact-sql"></a>sys.sp_drop_trusted_assembly (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

从服务器上的受信任程序集列表中删除程序集。

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>语法
```  
sp_drop_trusted_assembly 
    [ @hash = ] 'value'
```  

## <a name="arguments"></a>参数

[ @hash = ]"*value*"  
要从服务器的受信任程序集列表中删除的程序集的 SHA2_512 哈希值。 即使程序集未签名或数据库未标记为可信，也可以在启用 clr 严格安全时加载受信任的程序集。

## <a name="remarks"></a>备注  

此过程从 sys.databases 中删除程序集[。 trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)。

## <a name="permissions"></a>权限

要求具有固定服务器`sysadmin`角色或`CONTROL SERVER`权限的成员身份。

## <a name="examples"></a>示例  

下面的示例从服务器的受信任程序集列表中删除程序集哈希。  

```  
EXEC sp_drop_trusted_assembly 
0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC; 
```  

## <a name="see-also"></a>另请参阅  
  [sys.sp_add_trusted_assembly](sys-sp-add-trusted-assembly-transact-sql.md) [trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) [DROP assembly &#40;transact-sql&#41;](../../t-sql/statements/drop-assembly-transact-sql.md) sp_add_trusted_assembly  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

