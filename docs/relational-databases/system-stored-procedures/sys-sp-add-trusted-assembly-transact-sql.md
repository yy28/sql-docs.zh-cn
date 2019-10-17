---
title: sys. sp_add_trusted_assembly （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_trusted_assembly_TSQL
- sp_add_trusted_assembly
- sys.sp_add_trusted_assembly_TSQL
- sys.sp_add_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_add_trusted_assembly
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb34a814780a46c12c65948bd0b552effaacda4d
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452868"
---
# <a name="syssp_add_trusted_assembly-transact-sql"></a>sys. sp_add_trusted_assembly （Transact-sql）  
[!INCLUDE[tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md.md)]

将程序集添加到服务器的受信任程序集的列表中。

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [transact-sql 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>语法
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>注释  

此过程将程序集添加到[trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)。

## <a name="arguments"></a>参数

[@hash =]"*value*"  
要添加到服务器的受信任程序集列表的程序集的 SHA2_512 哈希值。 即使程序集未签名或数据库未标记为可信，也可以在启用[CLR 严格安全](../../database-engine/configure-windows/clr-strict-security.md)时加载受信任的程序集。

[@description =]"*description*"  
程序集的可选用户定义说明。 Microsoft 建议使用规范名称对要信任的程序集的简单名称、版本号、区域性、公钥和体系结构进行编码。 此值在公共语言运行时（CLR）端唯一标识程序集，与 sys.databases 中的 clr_name 值相同。 

## <a name="permissions"></a>Permissions

需要 `sysadmin` 固定服务器角色的成员身份或 `CONTROL SERVER` 权限。

## <a name="examples"></a>示例  

下面的示例将名为 `pointudt` 的程序集添加到服务器的受信任程序集的列表中。 可以从[sys.databases](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)获取这些值。     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>另请参阅  
  [sys. sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY (Transact-SQL)](../../t-sql/statements/create-assembly-transact-sql.md)  
  [CLR 严格安全性](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

