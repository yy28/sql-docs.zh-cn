---
title: ASSEMBLYPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASSEMBLYPROPERTY_TSQL
- ASSEMBLYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASSEMBLYPROPERTY statement
- assemblies [CLR integration], properties
ms.assetid: cf03d1b1-724c-48bf-a8df-3fe2586b150a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ac25131e24aa89253abfc13eac69a4a60d0b7aee
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68040288"
---
# <a name="assemblyproperty-transact-sql"></a>ASSEMBLYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

此函将返回有关程序集属性的信息。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
ASSEMBLYPROPERTY('assembly_name', 'property_name')  
```  
  
## <a name="arguments"></a>参数  
assembly_name   
程序集的名称。
  
property_name   
要检索其有关信息的属性的名称。 property_name 可以具有下列值之一  ：
  
|值|说明|  
|---|---|
|**CultureInfo**|程序集的区域设置。|  
|**PublicKey**|程序集的公钥或公钥令牌。|  
|**MvID**|由编译器生成的完整的程序集版本标识号。|  
|**VersionMajor**|由四部分组成的程序集版本标识号的主要组成部分（第一部分）。|  
|**VersionMinor**|由四部分组成的程序集版本标识号的次要组成部分（第二部分）。|  
|**VersionBuild**|由四部分组成的程序集版本标识号的内部版本组成部分（第三部分）。|  
|**VersionRevision**|由四部分组成的程序集版本标识号的修订版组成部分（第四部分）。|  
|**SimpleName**|程序集的简称。|  
|**体系结构**|程序集的处理器体系结构。|  
|**CLRName**|对程序集的简单名称、版本号、区域性、公钥以及体系结构进行编码的规范字符串。 该值唯一地标识公共语言运行时 (CLR) 端的程序集。|  
  
## <a name="return-type"></a>返回类型
**sql_variant**
  
## <a name="examples"></a>示例  
此示例假定在 `HelloWorld` 数据库中注册了 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 程序集。 有关详细信息，请参阅 [Hello World 示例](https://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7)。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ASSEMBLYPROPERTY ('HelloWorld' , 'PublicKey');  
```  
  
## <a name="see-also"></a>另请参阅
[CREATE ASSEMBLY (Transact-SQL)](../../t-sql/statements/create-assembly-transact-sql.md)  
[DROP ASSEMBLY (Transact-SQL)](../../t-sql/statements/drop-assembly-transact-sql.md)
  
  
