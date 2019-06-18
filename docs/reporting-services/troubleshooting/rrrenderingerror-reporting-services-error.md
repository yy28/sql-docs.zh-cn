---
title: rrRenderingError - Reporting Services 错误 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rrRenderingError
ms.assetid: 0751efc3-b81b-44ee-8aac-8560f86ca322
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1fcfe999a7cfaf41cc4b6b9fad437ea14dfe2613
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575557"
---
# <a name="rrrenderingerror---reporting-services-error"></a>rrRenderingError - Reporting Services 错误
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|rrRenderingError|  
|事件源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources.Strings|  
|组件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|消息正文|呈现报表时出错。 (rrRenderingError) %1|  
  
## <a name="explanation"></a>解释  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 无法呈现或导出报表时返回此消息。  
  
 当指定的 RDL 页大小无效时，通常会出现此消息，指明不支持该大小。 请指定有效的 RDL 页大小，然后重试。  
  
 当指定了不支持的单位类型时，通常会出现此消息，指明不支持 RDL 大小度量值。 有效的单位类型包括 cm、in、mm、pc 和 pt。 请指定有效的单位类型，然后重试。  
  
 为页大小指定了负值（例如 -5 cm）时，通常会出现此消息，指明不支持负的大小度量值。 请为页大小指定一个正数，然后重试。  
  
 当页大小度量值超出有效的页边距大小范围时，通常会出现此消息，指明指定的 RDL 大小超出范围。 请为页大小指定位于有效页边距大小范围内的度量值。  
  
 当 RDL 中指定的颜色无效时，通常会出现此消息，指明不支持指定的颜色。 请选择一种 RDL 支持的颜色，然后重试。  
  
 当指定的操作标签无效时，通常会出现此消息，指明只有使用单个操作时操作标签才是可选的，添加多个操作要求每个操作都有对应标签。 请为每个操作指定有效的操作标签。  
  
 当为数据类型指定了不正确的样式值时，通常会出现此消息，指明样式参数必须为特定类型。 RDL 规范中标识了可用作不同 RDL 元素的样式值的有效类型。 例如，不正确的背景颜色样式值为“2pt”，不正确的高度值为“true”。 请指定正确的值，然后重试。  
  
 当指定的边框样式无效时，通常会出现此消息，指明不支持该边框样式。 请指定受支持的边框样式，然后重试。  
  
 为图像报表项指定的 MIME 类型无效时，通常会出现此消息，指明不支持该图像 MIME 类型。 请为报表项指定受支持的 MIME 类型，然后重试。  
  
 当 Excel 工作表中的行数超出限制时，通常会出现此消息，指明行数超出了每页允许的最大行数。 Excel 最多支持 65,000 行。  
  
 当 Excel 工作表中的列数超出限制时，通常会出现此消息，指明列数超出了每页允许的最大列数。  
  
## <a name="user-action"></a>用户操作  
  
## <a name="internal-only"></a>仅内部  
  
