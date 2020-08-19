---
description: XML 源自定义属性
title: XML 源自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2f77a63b11636f2be16e3d7c81c5b902a95b2a84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425589"
---
# <a name="xml-source-custom-properties"></a>XML 源自定义属性

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  XML 源具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍 XML 源的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|说明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|用来访问 XML 数据的模式。|  
|UseInlineSchema|布尔|该值指示是否要在 XML 源中使用内联架构定义。 此属性的默认值为 **False**。|  
|XMLData|String|要从中检索 XML 数据的文件或变量。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
|XMLSchemaDefinition|String|架构定义文件 (.xsd) 的路径和文件名。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
  
 下表描述了 XML 源的输出的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|说明|  
|-------------------|---------------|-----------------|  
|RowsetID|String|标识与输出关联的行集的值。|  
  
 XML 源的输出列没有自定义属性。  
  
 有关详细信息，请参阅 [XML Source](../../integration-services/data-flow/xml-source.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
