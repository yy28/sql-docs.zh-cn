---
title: "OLE DB 架构行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [OLE DB]
- schema rowsets [Analysis Services], OLE DB
- OLE DB schema rowsets
- rowsets [Analysis Services], OLE DB
ms.assetid: ca2ee87a-ba04-4501-9125-33934c58ab31
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6467a1e54dba2ad8a4e88f1d892dfa2f3cd64381
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="ole-db-schema-rowsets"></a>OLE DB 架构行集
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持下列 OLE DB 架构行集。 使用**DISCOVER_ENUMERATORS**行集[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法来检查特定数据源提供程序是否支持行集。  
  
 在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 网站的 MSDN® Library 的“OLE DB Programmer's Reference”部分搜索“Schema Rowsets”主题，还可以找到有关这些行集的详细信息。  
  
 下表对此架构行集进行了说明。  
  
|行集|Description|  
|------------|-----------------|  
|**DBSCHEMA_ASSERTIONS**|标识在目录中定义的、给定用户拥有的断言。|  
|[DBSCHEMA_CATALOGS 行集](../../../analysis-services/schema-rowsets/ole-db/dbschema-catalogs-rowset.md) <sup>1</sup>|标识与可从数据库管理系统 (DBMS) 访问的目录关联的物理属性。 对于某些系统，如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Access，可能只存在一个目录。 对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，此行集将枚举在系统数据库中定义的所有目录（数据库）。|  
|**DBSCHEMA_CHARACTER_SETS**|标识在目录中定义的、给定用户可以访问的字符集。|  
|**DBSCHEMA_CHECK_CONSTRAINTS**|标识在目录中定义的、给定用户拥有的 CHECK 约束。|  
|**DBSCHEMA_CHECK_CONSTRAINTS_BY_TABLE**|标识在目录中定义的、给定用户拥有的、用于给定表的 CHECK 约束。|  
|**DBSCHEMA_COLLATIONS**|标识在目录中定义的、给定用户可以访问的字符排序规则。|  
|**DBSCHEMA_COLUMN_DOMAIN_USAGE**|标识在目录中定义的、依赖于在目录中定义的域并由给定用户拥有的列。|  
|**DBSCHEMA_COLUMN_PRIVILEGES**|标识在目录中定义的、给定用户可使用或授权的对表中列的特权。|  
|[DBSCHEMA_COLUMNS 行集](../../../analysis-services/schema-rowsets/ole-db/dbschema-columns-rowset.md) <sup>1</sup>|提供满足给定限制条件的所有列的列信息。|  
|**DBSCHEMA_CONSTRAINT_COLUMN_USAGE**|标识引用约束、唯一约束、CHECK 约束和断言使用的、在目录中定义的、给定用户拥有的列。|  
|**DBSCHEMA_CONSTRAINT_TABLE_USAGE**|标识引用约束、唯一约束、CHECK 约束和断言使用的、在目录中定义的、给定用户拥有的表。|  
|**DBSCHEMA_FOREIGN_KEYS**|标识由给定用户在目录中定义的外键列。 此架构行集是根据多个 ISO 架构视图生成的，便于非 SQL 编程人员使用。 如果支持，必须与相关的 ISO 视图同步此架构行集 (**REFERENTIAL_CONSTRAINTS**和**CONSTRAINT_COLUMN_USAGE**)。|  
|**DBSCHEMA_INDEXES**|标识在目录中定义的、给定用户拥有的索引。|  
|**DBSCHEMA_KEY_COLUMN_USAGE**|标识在目录中定义的、给定用户约束为键的列。|  
|**DBSCHEMA_PRIMARY_KEYS**|标识由给定用户在目录中定义的主键列。 此架构行集是根据一个 ISO 架构视图生成的，便于非 SQL 编程人员使用。 如果支持，必须将此架构行集同步与相关的 ISO 视图 (**CONSTRAINT_COLUMN_USAGE**)。|  
|**DBSCHEMA_PROCEDURE_COLUMNS**|返回有关由过程返回的行集中的列的信息。|  
|**DBSCHEMA_PROCEDURE_PARAMETERS**|返回有关过程的参数和返回代码的信息。|  
|**DBSCHEMA_PROCEDURES**|标识在目录中定义的、给定用户拥有的过程。 这是一个 OLE DB 扩展。|  
|[DBSCHEMA_PROVIDER_TYPES 行集](../../../analysis-services/schema-rowsets/ole-db/dbschema-provider-types-rowset.md) <sup>1</sup>|标识数据访问接口支持的（基本）数据类型。|  
|**DBSCHEMA_REFERENTIAL_CONSTRAINTS**|标识在目录中定义的、给定用户拥有的引用约束。|  
|**DBSCHEMA_SCHEMATA**|标识给定用户拥有的架构。|  
|**DBSCHEMA_SQL_LANGUAGES**|标识在目录中定义的、SQL 实现处理数据所支持的一致性级别、选项和方言。|  
|**DBSCHEMA_STATISTICS**|标识在目录中定义的、给定用户拥有的统计信息。<br /><br /> 此表不相关到**TABLE_STATISTICS**行集。|  
|**DBSCHEMA_TABLE_CONSTRAINTS**|标识在目录中定义、给定用户拥有的表约束。|  
|**DBSCHEMA_TABLE_PRIVILEGES**|标识在目录中定义的、给定用户可使用或授权的对表的特权。|  
|**DBSCHEMA_TABLE_STATISTICS**|描述访问接口中有关表的可用统计信息集。<br /><br /> 此行集不与相关**统计信息**行集。|  
|[DBSCHEMA_TABLES 行集](../../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md) <sup>1</sup>|标识的度量值组和维度中的表作为公开[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|**DBSCHEMA_TABLES_INFO** <sup>1</sup>|标识在目录中定义的、给定用户可以访问的表（包括视图）。|  
|**DBSCHEMA_TRANSLATIONS**|标识在目录中定义的、给定用户可以访问的字符转换。|  
|**DBSCHEMA_TRUSTEE**|枚举数据源的受信者。|  
|**DBSCHEMA_USAGE_PRIVILEGES**|标识**用法**上的目录中定义，可为或授予通过来给定用户的对象的权限。|  
|**DBSCHEMA_VIEW_COLUMN_USAGE**|标识在目录中定义的、给定用户可以访问的视图。|  
|**DBSCHEMA_VIEW_TABLE_USAGE**|标识查看的表所依赖的、在目录中定义并由给定用户拥有的表。|  
|**DBSCHEMA_VIEWS**|标识在目录中定义的、给定用户可以访问的视图。|  
  
 <sup>1</sup>指示 MSOLAP 数据源提供程序支持的架构行集[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XMLA 提供程序。  
  
## <a name="see-also"></a>另请参阅  
 [DISCOVER_ENUMERATORS 行集](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)   
 [Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
