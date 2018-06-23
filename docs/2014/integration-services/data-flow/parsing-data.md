---
title: 分析数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parsing [Integration Services]
- data parsing [Integration Services]
ms.assetid: 8893ea9d-634c-4309-b52c-6337222dcb39
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7517819f2cf6909cd95d76043519f78b06699b6c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128576"
---
# <a name="parsing-data"></a>分析数据
  包中的数据流在异类数据存储区之间提取和加载数据，这些存储区可能使用多种标准数据类型和自定义数据类型。 在数据流中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 源完成提取数据、分析字符串数据以及将数据转换成 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型的工作。 后续转换可以分析数据，以将其转换为不同的数据类型，或者创建不同数据类型的列副本。 在组件中使用的表达式还可以将参数和操作数转换为不同的数据类型。 最后，在将数据加载到数据存储区时，目标可以分析该数据，以将其转换为目标所使用的数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](integration-services-data-types.md)。  
  
## <a name="types-of-parsing"></a>分析类型  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了两种用于转换数据的分析类型：快速分析和标准分析。  
  
-   快速分析是一组简单快捷的分析例程，不支持区域设置特定的数据类型转换，仅支持最常用的日期和时间格式。 有关详细信息，请参阅 [Fast Parse](../fast-parse.md)。  
  
-   标准分析是一组功能齐全的分析例程，支持可在 Oleaut32.dll 和 Ole2dsip.dll 中使用的自动数据类型转换 API 所提供的所有数据类型转换。 有关详细信息，请参阅 [Standard Parse](../standard-parse.md)。  
  
  