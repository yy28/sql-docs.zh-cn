---
title: SQLXML 4.0 中的 DiffGrams 简介 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f7f94ac060cc4f76472c56c284636c09349261de
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48160767"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>SQLXML 4.0 中的 DiffGrams 简介
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
  
 **\<DataInstance >**  
 此元素的名称**DataInstance**，用于说明目的，本文档中。 例如，如果从.NET Framework 的值中的数据集生成 DiffGram**名称**将数据集属性将用作此元素的名称。 此块包含更改后的所有相关数据，可能包括尚未修改的数据。 DiffGram 处理逻辑将忽略此块中的元素，其**diffgr: haschanges**未指定属性。  
  
 **\<diffgr:before>**  
 此可选块包含必须更新或删除的原始记录实例（元素）。 正在修改 （更新或删除） 的所有数据库都表由 DiffGram 必须作为顶级元素出现在**\<之前 >** 块。  
  
 **\<diffgr:errors>**  
 DiffGram 处理逻辑将忽略此可选块。  
  
## <a name="diffgram-annotations"></a>DiffGram 批注  
 在 DiffGram 命名空间中定义这些批注 **"urn： 架构-microsoft-com:xml-diffgram-01"**:  
  
 **id**  
 使用此特性中的元素进行配对**\<之前 >** 并且 **\<DataInstance >** 块。  
  
 **hasChanges**  
 对于插入或更新操作，DiffGram 必须具有值指定此特性**插入**或**修改**。 如果不存在，此属性中的相应元素 **\<DataInstance >** 处理忽略执行逻辑和任何更新。 有关工作示例，请参阅[DiffGram 示例&#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)。  
  
 **parentID**  
 该属性在 DiffGram 中用于指定元素之间的父子关系。 此属性仅出现在\<之前 > 块。 应用更新时，SQLXML 将使用它。 在确定 DiffGram 中元素的处理顺序时，将使用该父子关系。  
  
## <a name="understanding-the-diffgram-processing-logic"></a>了解 DiffGram 处理逻辑  
 DiffGram 处理逻辑使用某些规则来确定操作是否是插入、更新或删除操作。 下表描述了这些规则。  
  
|运算|Description|  
|---------------|-----------------|  
|Insert|DiffGram 指示插入操作，当元素出现在 **\<DataInstance >** 块中但不是在相应**\<之前 >** 块，以及**diffgr: haschanges**指定属性 (**diffgr: haschanges = 插入**) 在元素上。 在这种情况下，DiffGram 插入中指定的记录实例 **\<DataInstance >** 到数据库中的块。<br /><br /> 如果**diffgr: haschanges**未指定属性、 处理逻辑将忽略该元素和不执行任何插入。 有关工作示例，请参阅[DiffGram 示例&#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)。|  
|Update|中的某个元素时，DiffGram 指示更新操作\<之前 > 没有相应的元素中的块 **\<DataInstance >** 块 （即，两个元素具有**diffgr: id**具有相同的值属性) 和**diffgr: haschanges**属性指定值**修改**中的元素上**\<DataInstance >** 块。<br /><br /> 如果**diffgr: haschanges**中的元素上未指定特性 **\<DataInstance >** 块中，处理逻辑返回错误。 有关工作示例，请参阅[DiffGram 示例&#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)。<br /><br /> 如果**diffgr: parentid**中指定**\<之前 >** 阻止，请通过指定的元素的父-子关系**parentID**中使用确定更新记录的顺序。|  
|DELETE|当元素出现在 DiffGram 指示删除操作**\<之前 >** 块中但不是在相应 **\<DataInstance >** 块。 在这种情况下，DiffGram 删除记录实例中指定**\<之前 >** 从数据库的块。 有关工作示例，请参阅[DiffGram 示例&#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)。<br /><br /> 如果**diffgr: parentid**中指定**\<之前 >** 阻止，请通过指定的元素的父-子关系**parentID**中使用确定删除记录的顺序。|  
  
> [!NOTE]  
>  参数无法传递到 DiffGrams。  
  
  
