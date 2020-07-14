---
title: 使用 XSINIL 生成 NULL 值对应的元素 | Microsoft Docs
description: 了解如何通过对 ELEMENTS 指令使用 XSINIL 参数，生成 NULL 值对应的 XML 元素。
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 7cf18eb7c5dea9a61988533205a3a64ab1ae3fd0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85638949"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>使用 XSINIL 参数生成 NULL 值对应的元素

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**ELEMENTS** 指令将构造 XML，其中每个列值映射到 XML 中的一个元素。 默认情况下，如果列值为 NULL，则不添加元素。 但通过对 ELEMENTS 指令指定可选的 **XSINIL** 参数，可以请求创建 NULL 值对应的元素。 在这种情况下，将为每个 NULL 列值返回一个元素，其 **xsi:nil** 属性被设置为 TRUE。  
  
## <a name="see-also"></a>另请参阅

[将 RAW 模式与 FOR XML 一起使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)

[SELECT - FOR 子句](../../t-sql/queries/select-for-clause-transact-sql.md)
