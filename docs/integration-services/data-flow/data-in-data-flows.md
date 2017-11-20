---
title: "数据中的数据流动 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data types [Integration Services]
- comparing data
- data types [Integration Services], data flow
- parsing [Integration Services]
- string comparisons
- data flow [Integration Services], data options
ms.assetid: 8a9d6186-eb52-48e3-997e-021f24d458a3
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: b9dd44fec24717695813010067b25d14c4a8036d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="data-in-data-flows"></a>数据流中的数据
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了用于数据流中的一组数据类型。  
  
## <a name="data-type-conversion"></a>数据类型转换  
 添加到数据流的源将源数据转换为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型。 后续转换可能将数据转换为不同的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型，而且根据数据加载于其上的数据存储区的类型，目标可能将最终的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型转换成目标数据存储区所需的数据类型。 有关详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 为将数据转换为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型，数据流组件对数据进行分析。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供两种类型的数据分析：快速分析和标准分析。 大多数数据流组件只能使用标准分析；但是，平面文件源和数据转换既可以使用快速分析，也可以使用标准分析。 有关详细信息，请参阅 [Parsing Data](../../integration-services/data-flow/parsing-data.md)。  
  
## <a name="data-type-comparison"></a>数据类型比较  
 很多转换都对数据值进行比较。 例如，聚合转换对值进行比较是为了聚合一组数据行中的值，排序转换对值进行比较是为了对值进行排序，而查找转换将值与单独的引用表中的值进行比较。 为指定应如何比较字符串，转换包括了一组比较选项，如是否忽略区分大小写、如何处理日语文本中的假名类型以及是否忽略字符串中的空格字符。 有关详细信息，请参阅 [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md)。  
  
 表达式计算器在计算变量、优先约束和转换使用的表达式时，也对数据值进行比较。  
  
## <a name="data-flow-troubleshooting"></a>数据流故障排除  
 将包部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录后，您可以在执行期间对包中的数据流进行分析，以检查性能或查找其他问题。 通过提供的标准报表，您可以查看包状态和历史记录，并查询提供了有关包执行的详细信息的数据库视图。 您还可以在执行期间动态添加和删除分流点以面向包的特定组件。 有关详细信息，请参阅 [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md)。  
  
  

