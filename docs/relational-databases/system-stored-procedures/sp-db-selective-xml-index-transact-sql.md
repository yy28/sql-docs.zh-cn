---
title: sp_db_selective_xml_index (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_selective_xml_index_TSQL
- sp_db_selective_xml_index
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_selective_xml_index procedure
ms.assetid: 017301a2-4a23-4e68-82af-134f3d4892b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8d951cff1b59be87bb8e8dc3d33b6fab50cdb87d
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130587"
---
# <a name="spdbselectivexmlindex-transact-sql"></a>sp_db_selective_xml_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库上启用和禁用选择性 XML 索引功能。 如果不带任何参数调用，则当在特定数据库上启用选择性 XML 索引时，存储过程返回 1。  
  
> [!NOTE]  
>  若要禁用选择性 XML 索引使用此存储的过程，必须将数据库置于简单恢复模式下使用[ALTER DATABASE SET 选项&#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)命令。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
  
      sys.sp_db_selective_xml_index[[ @db_name = ] 'db_name'],   
[[ @action = ] 'action']  
```  
  
## <a name="arguments"></a>参数  
 [ **@ db_name =** ] **'**_db_name_  
 要对其启用或禁用选择性 XML 索引的数据库名称。 如果*db_name*为 NULL，则假定为当前数据库。  
  
 [  **@action =** ] **'**_操作_  
 确定是启用还是禁用该索引。 如果 on 传递 true，off 或 false 之外的其他值，将引发错误。  
  
```  
  
Allowed values: 'on', 'off', 'true', 'false'  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **1**如果特定数据库上启用选择性 XML 索引。  
  
## <a name="examples"></a>示例  
  
### <a name="a-enable-selective-xml-index-functionality"></a>A. 启用选择性 XML 索引功能  
 下面的示例在当前数据库上启用选择性 XML 索引。  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'on';  
GO  
```  
  
 下面的示例在 AdventureWorks2012 数据库上启用选择性 XML 索引。  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'true';  
GO  
```  
  
### <a name="b-disable-selective-xml-index-functionality"></a>B. 禁用选择性 XML 索引功能  
 下面的示例在当前数据库上禁用选择性 XML 索引。  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'off';  
GO  
```  
  
 下面的示例在 AdventureWorks2012 数据库上禁用选择性 XML 索引。  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'false';  
GO  
```  
  
### <a name="c-detect-if-selective-xml-index-is-enabled"></a>C. 检测是否启用了选择性 XML 索引  
 下面的示例检测是否启用了选择性 XML 索引。 如果启用选择性 XML 索引，则返回 1。  
  
```  
EXECUTE sys.sp_db_selective_xml_index;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [选择性 XML 索引 (SXI)](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
