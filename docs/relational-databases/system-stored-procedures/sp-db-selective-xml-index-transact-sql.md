---
title: sp_db_selective_xml_index (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_db_selective_xml_index_TSQL
- sp_db_selective_xml_index
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_selective_xml_index procedure
ms.assetid: 017301a2-4a23-4e68-82af-134f3d4892b3
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3c70fcea339f1cb89026c3afed51f3e25d94f707
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spdbselectivexmlindex-transact-sql"></a>sp_db_selective_xml_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库上启用和禁用选择性 XML 索引功能。 如果不带任何参数调用，则当在特定数据库上启用选择性 XML 索引时，存储过程返回 1。  
  
> [!NOTE]  
>  若要禁用使用此存储的过程的选择性 XML 索引，必须将数据库置于简单恢复模式下使用[ALTER DATABASE SET 选项&#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)命令。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
  
      sys.sp_db_selective_xml_index[[ @db_name = ] 'db_name'],   
[[ @action = ] 'action']  
```  
  
## <a name="arguments"></a>参数  
 [ **@ db_name =** ] *****db_name*****  
 要对其启用或禁用选择性 XML 索引的数据库名称。 如果*db_name*为 NULL，则假定当前数据库。  
  
 [  **@action =** ] *****操作*****  
 确定是启用还是禁用该索引。 如果传递了“on”、“true”、“off”或“false”之外的其他值，则会引发错误。  
  
```  
  
Allowed values: 'on', 'off', 'true', 'false'  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **1**如果上一个特定的数据库启用了选择性 XML 索引。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [选择性 XML 索引 (SXI)](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
