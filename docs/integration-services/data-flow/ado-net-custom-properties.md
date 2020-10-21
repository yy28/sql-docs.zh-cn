---
description: ADO NET 自定义属性
title: ADO NET 自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e062a9ab-1e6b-4061-845a-4f8a0552b09d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 557b9c04bf89dfe4d2667689857c48102009c560
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194876"
---
# <a name="ado-net-custom-properties"></a>ADO NET 自定义属性

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **源自定义属性**  
  
 ADO NET 源具有自定义属性和所有数据流组件共有的属性。  
  
 下表介绍 ADO NET 源的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|说明|  
|-------------------|---------------|-----------------|  
|CommandTimeout|String|该值指定 SQL 命令超时之前等待的秒数。值为 0 时指示命令永远不会超时。|  
|SqlCommand|String|ADO NET 源可以用来提取数据的 SQL 语句。<br /><br /> 当包加载时，可以使用 ADO NET 源将使用的 SQL 语句动态更新此属性。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../integration-services/expressions/integration-services-ssis-expressions.md)和[在包中使用属性表达式](../../integration-services/expressions/use-property-expressions-in-packages.md)。|  
|AllowImplicitStringConversion|布尔|该值指示是否出现以下情况：<br /><br /> - 在外部元数据类型与字符串输出列类型（DT_WSTR 或 DT_NTEXT）之间存在不匹配时，未生成验证错误。<br /><br /> - 外部元数据类型隐式转换为输出列使用的字符串数据类型。<br /><br /> <br /><br /> 默认值为 TRUE。<br /><br /> 有关详细信息，请参阅 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)。|  
  
 ADO NET 源的输出和输出列没有自定义属性。  
  
 有关详细信息，请参阅 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)。  
  
 **目标自定义属性**  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目标具有自定义属性和所有数据流组件共有的属性。  
  
 下表介绍了 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目标的自定义属性。 所有属性均可读/写。 这些属性在 **“ADO NET 目标编辑器”** 中不可用，但可以使用 **“高级编辑器”** 进行设置。  
  
|属性|数据类型|说明|  
|--------------|---------------|-----------------|  
|BatchSize|Integer|向服务器发送的批中的行数。 值 **0** 指示批大小与内部缓冲区大小匹配。 此属性的默认值为 **0**。|  
|CommandTimeOut|Integer|SQL 命令在超时前可以运行的最大秒数。值 **0** 表示不限制时间。 此属性的默认值为 **0**。|  
|TableOrViewName|String|目标表或视图的名称。|  
  
 有关详细信息，请参阅 [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
