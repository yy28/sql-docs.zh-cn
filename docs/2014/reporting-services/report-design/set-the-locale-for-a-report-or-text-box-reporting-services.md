---
title: 设置报表或文本框的区域设置 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- locales [Reporting Services]
ms.assetid: df115b01-184b-47f0-b5ec-0ad965ff9bee
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1d2552c441a17f3d79c3db0d06a0b128618503d9
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59941653"
---
# <a name="set-the-locale-for-a-report-or-text-box-reporting-services"></a>设置报表或文本框的区域设置 (Reporting Services)
  报表或文本框的 **“语言”** 属性包含区域设置，该区域设置确定因语言和区域而异的默认报表数据显示格式，例如日期、货币或数值。 文本框的 **“语言”** 属性会覆盖报表的 **“语言”** 属性。 如果不为 **“语言”** 指定值，则 Reporting Services 将使用报表服务器所用操作系统的区域设置来发布报表，或使用报表创作计算机的区域设置来预览报表。  
  
 对于 HTML 报表，您可以覆盖默认 **“语言”** 值，而使用浏览器客户端的 HTTP 标头所指定的语言，方法是对报表或文本框的 **“语言”** 属性使用包含内置字段 User!Language 的表达式。  
  
 您还可以在 URL 中指定报表的 **“语言”** 属性。 有关详细信息，请参阅 [设置 URL 中的报表语言参数](../set-the-language-for-report-parameters-in-a-url.md)。  
  
### <a name="to-set-the-locale-for-a-report"></a>设置报表的区域设置  
  
1.  在“设计”视图中，单击报表设计图面的外部以选中该报表。  
  
2.  在“属性”窗格中，对于 **“语言”** 属性，键入或选择希望报表使用的语言。  
  
### <a name="to-set-the-locale-for-a-text-box"></a>设置文本框的区域设置  
  
1.  在“设计”视图中，选择要对其应用区域设置的文本框。  
  
2.  在“属性”窗格中，执行以下操作：  
  
    -   对于 **“日历”** 属性，键入或选择希望日期所要使用的日历。  
  
    -   对于 **“方向”** 属性，键入或选择写入文本的方向。  
  
    -   对于 **“语言”** 属性，键入或选择希望文本框所要使用的语言。 此值将覆盖报表的 **“语言”** 属性。  
  
    -   对于 **NumeralLanguage** 属性，键入或选择文本框中的数字所要使用的格式。  
  
    -   对于 **NumeralVariant** 属性，键入或选择要用于文本框中的数字的格式变量。  
  
    -   对于 **UnicodeBiDi** 属性，选择要在文本框中使用的双向嵌入级别。  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  
