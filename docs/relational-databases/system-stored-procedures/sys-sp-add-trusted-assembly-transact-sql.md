---
title: "sys.sp_add_trusted_assembly (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
ms.assetid: 
caps.latest.revision: 
author: tmullaney
ms.author: thmullan
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b634a990abcd9f763c851eaf1fbdde4d022ca25e
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="sysspaddtrustedassembly-transact-sql"></a>sys.sp_add_trusted_assembly (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

将程序集添加到的服务器的受信任程序集列表。

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>语法
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>注释  

此过程添加到的程序集[sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)。

## <a name="arguments"></a>参数

[ @hash = ] '*value*'  
要添加的服务器的受信任程序集列表中的程序集 SHA2_512 哈希值。 受信任的程序集可能会加载时[CLR 严格的安全](../../database-engine/configure-windows/clr-strict-security.md)启用，即使该程序集是无符号或数据库未标记为可信。

[ @description =] '*说明*  
程序集的可选用户定义描述。 Microsoft 建议使用将编码简单名称、 版本号、 区域性、 公钥，以及要信任的程序集的体系结构的规范名称。 此值唯一标识一侧公共语言运行时 (CLR) 程序集，并在 sys.assemblies clr_name 值相同。 

## <a name="permissions"></a>权限

要求的成员身份`sysadmin`固定的服务器角色或`CONTROL SERVER`权限。

## <a name="examples"></a>示例  

下面的示例添加名为的程序集`pointudt`到的服务器的受信任程序集的列表。 这些值是可从[sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)。     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>另请参阅  
  [sys.sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY (Transact-SQL)](../../t-sql/statements/create-assembly-transact-sql.md)  
  [CLR 严格的安全](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

