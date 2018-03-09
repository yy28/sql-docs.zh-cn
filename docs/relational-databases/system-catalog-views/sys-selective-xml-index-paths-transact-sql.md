---
title: "sys.selective_xml_index_paths (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xml_schema_attributes_TSQL
- xml_schema_attributes
- sys.xml_schema_attributes_TSQL
- sys.xml_schema_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_attributes catalog view
ms.assetid: 07a73d71-ec3e-4894-947a-5859ca62c606
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f71e46667c56b628965eab154af0c3e15c421f8
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysselectivexmlindexpaths-transact-sql"></a>sys.selective_xml_index_paths (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 开始，sys.selective_xml_index_paths 中的每行表示特定选择性 xml 索引的一个提升路径。  
  
 如果您使用以下语句对表的 xmlcol 创建一个选择性 xml 索引，  
  
```  
CREATE SELECTIVE XML INDEX sxi1 ON T(xmlcol)   
FOR ( path1 = '/a/b/c' AS XQUERY 'xs:string',  
      path2 = '/a/b/d' AS XQUERY 'xs:double'  
    )  
```  
  
 sys.selective_xml_index_paths 中将有对应索引 sxi1 的两个新行。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|包含 XML 列的表 ID。|  
|**index_id**|**int**|选择性 xml 索引的唯一 ID。|  
|**path_id**|**int**|提升的 XML 路径 ID。|  
|**path**|**nvarchar(4000)**|提升的路径。 例如，“/a/b/c/d/e”。|  
|**名称**|**sysname**|路径名称。|  
|**path_type**|**tinyint**|0 = XQUERY<br /><br /> 1 = SQL|  
|**path_type_desc**|**sysname**|基于**path_type** XQUERY' 或 'SQL' 的值。|  
|**xml_component_id**|**int**|在数据库中的 XML 架构组件的唯一 ID。|  
|**xquery_type_description**|**nvarchar(4000)**|指定的 xsd 类型的名称。|  
|**is_xquery_type_inferred**|**bit**|1 = 推断类型。|  
|**xquery_max_length**|**int**|最大长度（用 xsd 类型的字符表示）。|  
|**is_xquery_max_length_inferred**|**bit**|1 = 推断最大长度。|  
|**is_node**|**bit**|0 = node() 提示不存在。<br /><br /> 1 = 应用 node() 优化提示。|  
|**system_type_id**|**tinyint**|列的系统类型的 ID。|  
|**user_type_id**|**tinyint**|列的用户类型的 ID。|  
|**max_length**|**int**|类型的最大长度 （以字节为单位）。<br /><br /> -1 = 列数据类型为 varchar(max)、nvarchar(max)、varbinary(max) 或 xml。|  
|**精度**|**tinyint**|如果类型基于数值，则表示类型的最大精度。 否则为 0。|  
|**小数位数**|**tinyint**|如果类型基于数值，则表示类型的最大小数位数。 否则为 0。|  
|**collation_name**|**sysname**|如果类型基于字符，则表示类型排序规则的名称。 否则，为 NULL。|  
|**is_singleton**|**bit**|0 = SINGLETON 提示不存在。<br /><br /> 1 = 应用 SINGLETON 优化提示。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架构 &#40;XML 类型系统 &#41;目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
