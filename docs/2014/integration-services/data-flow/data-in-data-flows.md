---
title: 数据流中的数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- comparing data
- data types [Integration Services], data flow
- parsing [Integration Services]
- string comparisons
- data flow [Integration Services], data options
ms.assetid: 8a9d6186-eb52-48e3-997e-021f24d458a3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 225b6010e5d5a6c45a84d7e22272c4e5242906fd
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374145"
---
# <a name="data-in-data-flows"></a>数据流中的数据
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了用于数据流中的一组数据类型。  
  
## <a name="data-type-conversion"></a>数据类型转换  
 添加到数据流的源将源数据转换为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型。 后续转换可能将数据转换为不同的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型，而且根据数据加载于其上的数据存储区的类型，目标可能将最终的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型转换成目标数据存储区所需的数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](integration-services-data-types.md)。  
  
 为将数据转换为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型，数据流组件对数据进行分析。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供两种类型的数据分析：快速分析和标准分析。 大多数数据流组件只能使用标准分析；但是，平面文件源和数据转换既可以使用快速分析，也可以使用标准分析。 有关详细信息，请参阅 [Parsing Data](parsing-data.md)。  
  
## <a name="data-type-comparison"></a>数据类型比较  
 很多转换都对数据值进行比较。 例如，聚合转换对值进行比较是为了聚合一组数据行中的值，排序转换对值进行比较是为了对值进行排序，而查找转换将值与单独的引用表中的值进行比较。 为指定应如何比较字符串，转换包括了一组比较选项，如是否忽略区分大小写、如何处理日语文本中的假名类型以及是否忽略字符串中的空格字符。 有关详细信息，请参阅 [Comparing String Data](comparing-string-data.md)。  
  
 表达式计算器在计算变量、优先约束和转换使用的表达式时，也对数据值进行比较。  
  
## <a name="data-flow-troubleshooting"></a>数据流故障排除  
 将包部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录后，您可以在执行期间对包中的数据流进行分析，以检查性能或查找其他问题。 通过提供的标准报表，您可以查看包状态和历史记录，并查询提供了有关包执行的详细信息的数据库视图。 您还可以在执行期间动态添加和删除分流点以面向包的特定组件。 有关详细信息，请参阅 [数据流分析](data-flow.md)。  
  
  
