---
title: 使用 XSINIL 参数生成 NULL 值对应的元素 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 602de12b5aa9be8997fbd49a2f23e0b73444aac0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061218"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>使用 XSINIL 参数生成 NULL 值对应的元素
  **ELEMENTS** 指令将构造 XML，其中每个列值映射到 XML 中的一个元素。 如果列值为 NULL，则不添加元素。 通过对 ELEMENTS 指令指定可选的 **XSINIL** 参数，可以请求创建 NULL 值对应的元素。 在这种情况下，将为每个 NULL 列值返回一个元素，其 **xsi:nil** 属性被设置为 TRUE。  
  
## <a name="see-also"></a>另请参阅  
 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md)  
  
  
