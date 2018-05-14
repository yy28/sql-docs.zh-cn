---
title: DISCOVER_CSDL_METADATA 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ca80c243a7ee9c001f079f21908f803a99b75e1f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="discovercsdlmetadata-rowset"></a>DISCOVER_CSDL_METADATA 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  返回有关 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据模型（表格或多维）的信息，同时提供 CSDLBI 格式（带 BI 注释的概念性架构定义语言）的模型定义。 CSDLBI 基于 CSDL，CSDL 是实体数据框架使用的 XML 架构，用于在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器和 [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] 客户端之间进行通信。 商业智能 (BI) 注释提供有关表格模型以及其中对象的其他元数据。 有关表格数据模型的详细信息，请参阅[用于商业智能的 CSDL 批注 (CSDLBI)](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)。  
  
 该命令的安全上下文影响返回的行集。 对于 Analysis Services 实例的读取权限是从服务器获取 CSDL 定义所必需的。  
  
 发出行集请求的客户端的语言标识符包括在命令的连接字符串中，并且影响作为行集的一部分返回的若干属性中显示的语言。  有关语言标识符可影响的属性和说明的信息，请参阅“备注”部分。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_CSDL_METADATA** 行集包含以下列。  
  
|**列名**|**类型指示符**|**限制**|**Description**|  
|---------------------|------------------------|---------------------|---------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|是|指定请求 CSDLBI 说明的数据库的名称。 如果省略，则使用当前数据库。<br /><br /> 这一限制对所有模型类型都是必需的。|  
|**PERSPECTIVE_ID**|**DBTYPE_WSTR**|是|指定已对由 CATALOG_NAME 指定的模型定义的透视的 ID。<br /><br /> 可选限制。 适用于所有模型类型。|  
|**PERSPECTIVE_NAME**|**DBTYPE_WSTR**|是|指定已对 CATALOG_NAME 指定的模型定义的透视的名称。<br /><br /> 当表格模型包含透视或多维解决方案包含多个多维数据集或透视时，此限制是必需的。|  
|**元数据**|**DBTYPE_WSTR**|否|根据 CSDLBI 架构，包含数据源的 XML 定义及其属性的字符串。|  
|**CUBE_ID**|**DBTYPE_WSTR**|是|字符串标识符。<br /><br /> 此限制对于多维数据库是可选的。 如果多个多维数据集可用并且忽略限制，则返回默认多维数据集。|  
  
## <a name="remarks"></a>注释  
 DISCOVER_CSDL_METADATA 具有以下要求：  
  
-   如果数据库未使用 CATALOG_NAME 限制指定，DISCOVER 请求将失败。  
  
-   对于表格模型，如果模型中有多个透视，则需要透视 ID。  
  
-   对于多维模型，则同时需要目录名称和多维数据集（透视）名称。  
  
-   如果透视作为限制提供，则对该模型将返回相同的 CSDL 行集。 但是，模型中存在但未包含在指定透视中的任何对象都标记为 **Hidden** = True。  
  
-   对于表和列，DISCOVER 请求始终从多维数据集维度输出值。 如果未设置多维数据集属性，则该请求将从维度返回值。  
  
-   DISCOVER 请求不能返回包含语义错误的任何度量值或计算列。  
  
-   DISCOVER 请求将不返回不具有属性值的对象的任何信息。 DISCOVER 请求还将不返回使用默认值的属性的值。  
  
 在行集中返回的 XML 字符串可能包含以下特定于语言的属性或值。 例如，如果您从其 LCID 为 0403（加泰罗尼亚西班牙语）的客户端发出该行集请求，则该属性将返回适用于加泰罗尼亚西班牙语的以下值。 如果翻译在该服务器上不可用，则返回该服务器的默认语言。  
  
-   Caption  
  
-   Qualifier  
  
-   SortDirection  
  
-   IsRightToLeft  
  
## <a name="example"></a>示例  
 **表格**  
  
 以下 XMLA 查询返回 AdventureWorks 2012 表格模型示例的 CSDL 表示形式。 每个表格解决方案只能包含一个模型，因此，PERSPECTIVE_NAME 限制可能保留为空。 但是，这个模型包含多个透视。  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>AdventureWorks2012Tabular</CATALOG_NAME>  
                <PERSPECTIVE_NAME>EMPLOYEE</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
</Discover>  
  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 以下 XMLA 查询返回 Contoso Operations 多维数据集的 CSDLBI 表示形式。 要查询多维数据库，则需要 VERSION 限制。 Contoso Retail 数据库包含两个多维数据集，因此通过使用 PERSPECTIVE_NAME 限制来引用 Operations 多维数据集。  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>Contoso_Retail</CATALOG_NAME>  
                <PERSPECTIVE_NAME>Operation</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
 </Discover>  
  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|3444B255-171E-4cb9-AD98-19E57888A75F|  
|ADOMDNAME|Csdl|  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Business Intelligence & #40; 有关的 CSDL 批注CSDLBI & #41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
  
