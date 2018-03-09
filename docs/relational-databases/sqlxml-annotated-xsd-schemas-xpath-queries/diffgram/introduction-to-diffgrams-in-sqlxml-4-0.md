---
title: "SQLXML 4.0 中的 Diffgram 简介 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5743cbab13add72e27351c74424e09bc028496d9
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>SQLXML 4.0 中的 DiffGrams 简介
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
本主题提供对 DiffGrams 的简要介绍。  
  
## <a name="diffgram-format"></a>DiffGram 格式  
 这是常规 DiffGram 格式：  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
   <DataInstance>  
      ...  
   </DataInstance>  
   [<diffgr:before>  
        ...  
   </diffgr:before>]  
  
   [<diffgr:errors>  
        ...  
   </diffgr:errors>]  
</diffgr:diffgram>  
```  
  
 DiffGram 格式由这些块组成：  
  
 **\<DataInstance>**  
 此元素的名称**DataInstance**，用于说明目的，本文档中。 例如，如果从.NET Framework 中的值中的数据集生成 DiffGram**名称**数据集的属性将用作此元素的名称。 此块包含更改后的所有相关数据，可能包括尚未修改的数据。 DiffGram 处理逻辑忽略此块中的元素为其**diffgr:hasChanges**未指定属性。  
  
 **\<diffgr:before>**  
 此可选块包含必须更新或删除的原始记录实例（元素）。 所有数据库都表 （更新或删除） 正在修改由 DiffGram 必须中显示为顶级元素**\<之前 >**块。  
  
 **\<diffgr:errors>**  
 DiffGram 处理逻辑将忽略此可选块。  
  
## <a name="diffgram-annotations"></a>DiffGram 批注  
 在 DiffGram 命名空间中定义这些批注**"urn： 架构-microsoft-com:xml-diffgram-01"**:  
  
 **id**  
 此属性用于中的元素配对**\<之前 >**和 **\<DataInstance >**块。  
  
 **hasChanges**  
 对于插入或更新操作，在 DiffGram 必须具有值指定此属性**插入**或**修改**。 如果此属性不存在中的相应元素 **\<DataInstance >**忽略处理的执行逻辑和任何更新。 有关工作示例，请参阅[DiffGram 示例 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 **parentID**  
 该属性在 DiffGram 中用于指定元素之间的父子关系。 此属性仅在出现\<之前 > 块。 应用更新时，SQLXML 将使用它。 在确定 DiffGram 中元素的处理顺序时，将使用该父子关系。  
  
## <a name="understanding-the-diffgram-processing-logic"></a>了解 DiffGram 处理逻辑  
 DiffGram 处理逻辑使用某些规则来确定操作是否是插入、更新或删除操作。 下表描述了这些规则。  
  
|运算|Description|  
|---------------|-----------------|  
|Insert|DiffGram 表示插入操作，当元素出现在 **\<DataInstance >**块，但不是在相应**\<之前 >**块和**diffgr:hasChanges**指定属性 (**diffgr:hasChanges = 插入**) 元素上。 在这种情况下，在 DiffGram 插入中指定的记录实例 **\<DataInstance >**到数据库的块。<br /><br /> 如果**diffgr:hasChanges**未指定属性、 通过处理逻辑，将忽略该元素和不执行任何插入。 有关工作示例，请参阅[DiffGram 示例 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).|  
|Update|DiffGram 表示更新操作中的某个元素时\<之前 > 没有中的相应元素的块 **\<DataInstance >**块 （这就是，这两个元素具有**diffgr: id**具有相同值的属性) 和**diffgr:hasChanges**属性指定值**修改**中的元素上**\<DataInstance >**块。<br /><br /> 如果**diffgr:hasChanges**中的元素上未指定属性 **\<DataInstance >**块中，通过处理逻辑返回一个错误。 有关工作示例，请参阅[DiffGram 示例 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> 如果**diffgr: parentid**中指定**\<之前 >**一直阻止，请通过指定的元素的父-子关系**parentID**中使用确定更新记录的顺序。|  
|删除|DiffGram 指示删除操作时元素出现在**\<之前 >**块，但不是在相应 **\<DataInstance >**块。 在这种情况下，在 DiffGram 删除中指定的记录实例**\<之前 >**从数据库的块。 有关工作示例，请参阅[DiffGram 示例 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> 如果**diffgr: parentid**中指定**\<之前 >**一直阻止，请通过指定的元素的父-子关系**parentID**中使用确定在其中删除记录的顺序。|  
  
> [!NOTE]  
>  参数无法传递到 DiffGrams。  
  
  
