---
title: 维度处理目标自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f4dae4c9661e8a04e34b5d2b78ccdd0f556bfa7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015077"
---
# <a name="dimension-processing-destination-custom-properies"></a>维度处理目标自定义属性
  维度处理目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍了纬度处理目标的自定义属性。 所有属性均可读/写。  
  
|“属性”|数据类型|Description|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的实例或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的连接字符串。|  
|KeyDuplicate|Integer（枚举）|UseDefaultConfiguration 时`False`，一个值，指示如何处理重复键错误。 可能的值为`IgnoreError`(0)， `ReportAndContinue` (1) 和`ReportAndStop`(2)。 此属性的默认值是`IgnoreError`(0)。|  
|KeyErrorAction|Integer（枚举）|UseDefaultConfiguration 时`False`，一个值，指示如何处理键错误。 可能的值为 `ConvertToUnknown` (0) 和 `DiscardRecord` (1)。 此属性的默认值是`ConvertToUnknown`(0)。|  
|KeyErrorLimit|Integer|UseDefaultConfiguration 时`False`，启用的键错误的上限。|  
|KeyErrorLimitAction|Integer（枚举）|UseDefaultConfiguration 时`False`，一个值，指示要执行时的操作`KeyErrorLimit`为止。 可能的值为`StopLogging`(1) 和`StopProcessing`(0)。 此属性的默认值是`StopProcessing`(0)。|  
|KeyErrorLogFile|String|UseDefaultConfiguration 时`False`，错误日志文件的路径和文件名称。|  
|“KeyNotFound”|Integer（枚举）|UseDefaultConfiguration 时`False`，一个值，指示如何处理缺少键错误。 可能的值为`IgnoreError`(0)， `ReportAndContinue` (1) 和`ReportAndStop`(2)。 此属性的默认值是`IgnoreError`(0)。|  
|NullKeyConvertedToUnknown|Integer（枚举）|UseDefaultConfiguration 时`False`，一个值，指示如何处理 null 键转换为未知值。 可能的值为`IgnoreError`(0)， `ReportAndContinue` (1) 和`ReportAndStop`(2)。 此属性的默认值是`IgnoreError`(0)。|  
|NullKeyNotAllowed|Integer（枚举）|UseDefaultConfiguration 时`False`，一个值，指示如何处理不允许 null 值。 可能的值为`IgnoreError`(0)， `ReportAndContinue` (1) 和`ReportAndStop`(2)。 此属性的默认值是`IgnoreError`(0)。|  
|ProcessType|Integer（枚举）|转换使用的维度处理类型。 值为 `ProcessAdd` (1)（增量）、`ProcessFull` (0) 和 `ProcessUpdate` (2)。|  
|UseDefaultConfiguration|Boolean|一个指定转换是否使用默认错误配置的值。 如果此属性为`False`，则转换包含有关错误处理的信息。|  
  
 维度处理目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [Dimension Processing Destination](dimension-processing-destination.md)。  
  
## <a name="see-also"></a>请参阅  
 [Common Properties](../common-properties.md)  
  
  