---
title: 维度处理目标自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f37c189f4d71aa9201f87a0215a3e0fee331216c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437834"
---
# <a name="dimension-processing-destination-custom-properies"></a>维度处理目标自定义属性
  维度处理目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍了纬度处理目标的自定义属性。 所有属性均可读/写。  
  
|properties|数据类型|说明|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的实例或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的连接字符串。|  
|KeyDuplicate|Integer（枚举）|当 UseDefaultConfiguration 为时 `False` ，指示如何处理重复键错误的值。 可能的值为 `IgnoreError` (0)、`ReportAndContinue` (1) 和 `ReportAndStop` (2)。 此属性的默认值为 `IgnoreError` (0)。|  
|KeyErrorAction|Integer（枚举）|当 UseDefaultConfiguration 为时 `False` ，指示如何处理键错误的值。 可能的值为 `ConvertToUnknown` (0) 和 `DiscardRecord` (1)。 此属性的默认值为 `ConvertToUnknown` (0)。|  
|KeyErrorLimit|Integer|当 UseDefaultConfiguration 为时 `False` ，启用的键错误的上限。|  
|KeyErrorLimitAction|Integer（枚举）|当 UseDefaultConfiguration 为时 `False` ，指示达到时要执行的操作的值 `KeyErrorLimit` 。 可能的值为 `StopLogging` (1) 和 `StopProcessing` (0)。 此属性的默认值为 `StopProcessing` (0)。|  
|KeyErrorLogFile|String|当 UseDefaultConfiguration 为时 `False` ，为错误日志文件的路径和文件名。|  
|KeyNotFound|Integer（枚举）|当 UseDefaultConfiguration 为时 `False` ，指示如何处理缺少的键错误的值。 可能的值为 `IgnoreError` (0)、`ReportAndContinue` (1) 和 `ReportAndStop` (2)。 此属性的默认值为 `IgnoreError` (0)。|  
|NullKeyConvertedToUnknown|Integer（枚举）|当 UseDefaultConfiguration 为时 `False` ，指示如何处理转换为未知值的 null 键的值。 可能的值为 `IgnoreError` (0)、`ReportAndContinue` (1) 和 `ReportAndStop` (2)。 此属性的默认值为 `IgnoreError` (0)。|  
|NullKeyNotAllowed|Integer（枚举）|当 UseDefaultConfiguration 为时 `False` ，指示如何处理不允许的 null 值。 可能的值为 `IgnoreError` (0)、`ReportAndContinue` (1) 和 `ReportAndStop` (2)。 此属性的默认值为 `IgnoreError` (0)。|  
|ProcessType|Integer（枚举）|转换使用的维度处理类型。 值为 `ProcessAdd` (1)（增量）、`ProcessFull` (0) 和 `ProcessUpdate` (2)。|  
|UseDefaultConfiguration|Boolean|一个指定转换是否使用默认错误配置的值。 如果此属性为 `False`，则转换包含有关错误处理的信息。|  
  
 维度处理目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [Dimension Processing Destination](dimension-processing-destination.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Common Properties](../common-properties.md)  
  
  
