---
title: 快速分析 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- fast parse [Integration Services]
ms.assetid: 6688707d-3c5b-404e-aa2f-e13092ac8d95
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d080df993035bc34783bb39991d80d6a8e692618
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58373814"
---
# <a name="fast-parse"></a>Fast Parse
  快速分析提供一组快速、简单的数据分析例程。 这些例程是不区分区域设置的，并且它们只支持日期、时间和整数格式的一个子集。  
  
## <a name="requirements-and-limitations"></a>要求和限制  
 通过实现快速分析，包失去了以特定于区域设置的格式和很多常用的 ISO 8601 基本及扩展格式来转换日期、时间和数值数据的能力，但包的性能得到了提高。 例如，快速分析仅支持最常用的日期格式表示形式（比如，YYYYMMDD 和 YYYY-MM-DD），不执行区域设置特定的分析，不能识别货币数据中的特殊字符，也不能转换对整数的十六进制或科学表示形式。  
  
 快速分析仅在使用平面文件源或数据转换时才可用。 包的性能可能会得到显著提高，您应尽可能考虑在这些数据流组件中使用快速分析。  
  
 如果包中的数据流需要受区域设置影响的分析，则应使用标准分析，而不是快速分析。 例如，快速分析不能识别受区域设置影响的数据，包括小数符号（如逗号）、与“年-月-日”格式不同的日期格式以及货币符号。  
  
 快速分析不能识别隐含一个或多个日期部分（如世纪、年、月）的截断的表示形式。 例如，快速分析既不能识别“**-YYMM**”格式（指定某个隐含世纪中的年和月），也不能识别“**--MM**”格式（指定某个隐含年中的月）。 但是，某些降低了精度的表示形式可以被识别。 例如，快速分析可以识别“hhmm;”格式（仅指示时和分）和“**YYYY**”格式（仅指示年）。  
  
 快速分析在列级指定。 在平面文件源和数据转换中，可以指定对输出列进行快速分析。 输入和输出可以同时包含受区域设置影响的列和不受区域设置影响的列。  
  
 有关快速分析支持的数据格式的详细信息，请参阅 [Numeric Data Formats](../../2014/integration-services/numeric-data-formats.md) 和 [Date and Time Formats](../../2014/integration-services/date-and-time-formats.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [设置快速分析](../../2014/integration-services/set-fast-parse.md)  
  
  
