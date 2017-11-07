---
title: "DISCOVER_CALC_DEPENDENCY 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
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
- DISCOVER_CALC_DEPENDENCIES rowset
ms.assetid: f39dde72-fa5c-4c82-8b4e-88358aa2e422
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 86f0ed45ced35aba884f05284f886334d250694d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="discovercalcdependency-rowset"></a>DISCOVER_CALC_DEPENDENCY 行集
  报告计算之间的依赖关系以及这些计算中引用的对象。 您可以在客户端应用程序中使用这些信息来报告与复杂公式相关的问题，或者在删除或修改相关对象时发出警告。 您还可以使用行集提取在度量值或计算列中使用的 DAX 表达式。  
  
 **适用于：** 表格模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_CALC_DEPENDENCY** 行集包含以下列。 该表还指定数据类型，指示是否可通过限制列来限制返回的行，并提供每列的说明。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|是|指定包含要请求对其进行依赖关系分析的对象的数据库名称。 如果省略，则使用当前数据库。<br /><br /> 可通过使用此列对 **DISCOVER_DEPENDENCY_CALC** 行集进行限制。|  
|**对象类型**|**DBTYPE_WSTR**|是|指示要请求对其进行依赖关系分析的对象的类型。 该对象必须是以下类型之一：<br /><br /> **ACTIVE_RELATIONSHIP**：处于活动状态的关系<br /><br /> **CALC_COLUMN**：计算列<br /><br /> **HIERARCHY**：层次结构<br /><br /> **MEASURE**：度量值<br /><br /> **RELATIONSHIP**：关系<br /><br /> **KPI**：KPI（关键绩效指标）<br /><br /> <br /><br /> 请注意， **DISCOVER_DEPENDENCY_CALC**行集可通过使用此列来限制。|  
|**查询**|**DBTYPE_WSTR**|是|对于在 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 中创建的表格模型，您可以包含 DAX 查询或表达式，以显示该查询或表达式的依赖关系图。 QUERY 限制为客户端应用程序提供了一种方法，以确定 DAX 查询所使用的对象。<br /><br /> 可在 XMLA 中或 DMV 查询的 WHERE 子句中指定 **QUERY** 限制。 有关详细信息，请参阅示例部分。|  
|**表**|**DBTYPE_WSTR**||要为其生成依赖关系信息的对象所在的表的名称。|  
|**对象**|**DBTYPE_WSTR**||要为其生成依赖关系信息的对象的名称。 如果该对象是某一度量值或计算列，则使用该度量值的名称。 如果该对象是某一关系，则为包含参与该关系的列的表（或者多维数据集维度）的名称。|  
|**表达式**|**DBTYPE_WSTR**||包含要寻找其依赖关系的对象的公式。|  
|**REFERENCED_OBJECT_TYPE**|**DBTYPE_WSTR**||返回具有对引用对象的依赖关系的对象的类型。 返回的对象可以是以下类型之一：<br /><br /> **CALC_COLUMN**：计算列<br /><br /> **COLUMN**：数据列<br /><br /> **MEASURE**：度量值<br /><br /> **RELATIONSHIP**：关系<br /><br /> **KPI**：KPI（关键绩效指标）|  
|**REFERENCED_TABLE**|**DBTYPE_ WSTR**||包含依赖对象的表的名称。|  
|**REFERENCED_OBJECT**|**DBTYPE_ WSTR**||具有对引用对象的依赖关系的对象的名称。 对于度量值和计算列，则为该度量值或列的名称。 对于关系，则为包含依赖对象的表（或多维数据集维度）的完全限定名称。|  
|**REFERENCED_EXPRESSION**|**DBTYPE_WSTR**||依赖于所引用对象的计算列或度量值中的公式。|  
  
## <a name="example"></a>示例  
 **基本语法**  
  
 下面的查询是一个简单的 DMV 查询，该查询使用当前连接上的默认数据库返回此行集中所有列的值。 您可以在 MDX 查询窗口中运行此查询，并在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 中查看其结果。 你也可以按照中所述的技术[从 Excel 查询 Power Pivot Dmv](http://go.microsoft.com/fwlink/?LinkID=235146)若要在 Excel 中查看 DMV 查询结果。  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
```  
  
## <a name="example"></a>示例  
 **对结果进行排序**  
  
 添加 ORDER BY 以按表或其他列对行集进行排序。  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY ORDER BY [TABLE] ASC  
```  
  
## <a name="example"></a>示例  
 **使用 WHERE 子句进行筛选**  
  
 下一个查询说明如何使用 WHERE 子句添加限制。 以下各列在 WHERE 子句中可以用作查询筛选器： **Database_Name**、 **Object_Type**和 **Query**。  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'RELATIONSHIP' OR OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
## <a name="example"></a>示例  
 **度量值和计算的列，若要查看基础 DAX 表达式进行筛选**  
  
 在此查询中，您可以只选择该度量值或计算列，然后查看计算中使用的 DAX 表达式。 EXPRESSION 列包含 DAX 表达式。 如果您使用 DISCOVER_CALC_DEPENDENCY 来提取模型中使用的 DAX 表达式，使用此查询即可实现此目的。 它将返回模型中使用的所有表达式，按升序排序。  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'MEASURE' OR OBJECT_TYPE = 'CALC_COLUMN' ORDER BY [EXPRESSION] ASC  
```  
  
## <a name="example"></a>示例  
 **使用 QUERY 进行筛选**  
  
 使用 QUERY 限制，您可以提供 DAX 查询，以查看该查询中使用的所有对象。 请考虑一个简单查询，如“Evaluate Customer”。 顾名思义，此查询返回客户数据行，其中行的构成基于 Customer 表中的列。 如果您现在运行带有 QUERY 限制（“Evaluate Customer”）的 DISCOVER_CALC_DEPENDENCY，则会获得该查询中所使用的列（或对象）。 在此情况下，它是 Customer 表中列的列表。  
  
 下一组查询演示了 QUERY 限制的语法。 您可以对 [AdventureWorks 表格模型 (SQL Server 2012)](http://msftdbprodsamples.codeplex.com/releases/view/55330) 运行这些查询以查看结果集。  
  
 第一个查询显示如何为包含空格的对象名称指定 QUERY 限制。 第二个查询（自 [通过 OLE DB 和 ADOMD.NET 执行 DAX 查询](http://go.microsoft.com/fwlink/?LinkId=254329)中借用）是一个更复杂的查询，其中包含来自多个表的对象。  
  
> [!NOTE]  
>  尽管查询看起来使用了双引号，但实际上使用的是两个单引号。 有一对单引号包含评估\<Tablename >，并且需要通过使用双重它们转义的表名称两边所用单引号引起来。 只有包含空格的表名称才需要在表名称周围加上单引号。  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE ''Reseller Sales'''  
```  
  
```  
SELECT * from $system.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE CALCULATETABLE(VALUES(''Product Subcategory''[Product Subcategory Name]), ''Product Category''[Product Category Name] = "Bikes")'  
```  
  
## <a name="example"></a>示例  
 **QUERY 限制 XMLA 示例**  
  
 您可以使用 XMLA Discover 命令来返回表中的查询对象。 XMLA 将结果作为原始 XML 返回。 您可以使用 ADOMD.NET 以更便于阅读的格式分析结果。  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>DISCOVER_CALC_DEPENDENCY</RequestType>  
     <Restrictions>  
        <RestrictionList>  
            <QUERY>Evaluate 'Reseller Sales'</QUERY>  
        </RestrictionList>  
    </Restrictions>  
    <Properties />  
</Discover>  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|a07ccd46-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|DependencyGraph|  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [使用动态管理视图 &#40; Dmv &#41;监视 Analysis Services](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  

