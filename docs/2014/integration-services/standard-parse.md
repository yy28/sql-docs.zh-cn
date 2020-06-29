---
title: 标准分析 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- standard parse [Integration Services]
- locales [Integration Services]
ms.assetid: dfe835b1-ea52-4e18-a23a-5188c5b6f013
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7cacff710870d372d6bbf8345e05397857c13a00
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85420784"
---
# <a name="standard-parse"></a>Standard Parse
  标准分析是一组受区域设置影响的分析例程，这些例程支持 Oleaut32.dll 和 Ole2dsip.dll 中可用的自动数据类型转换 API 所提供的全部数据类型转换。 标准分析相当于 OLE DB 分析 API。  
  
 标准分析支持国际数据的数据类型转换，且快速分析不支持数据格式时应使用标准分析。 有关自动化数据类型转换 API 的详细信息，请参阅 [MSDN Library](https://go.microsoft.com/fwlink/?LinkId=79427)中的“Data Type Conversion APIs”（数据类型转换 API）。  
  
## <a name="see-also"></a>另请参阅  
 [Fast Parse](../../2014/integration-services/fast-parse.md)  
  
  
