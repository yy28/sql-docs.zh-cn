---
title: 自动填充 IPD |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1591843667ef01c6c88f5dfafb734f044679b2d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909831"
---
# <a name="automatic-population-of-the-ipd"></a>自动填充 IPD
在准备好参数化查询后，某些驱动程序能够设置 IPD 字段。 描述符字段会自动填充有关参数的信息，包括数据类型、精度、小数位数和其他特征。 这等效于支持**SQLDescribeParam**。 当应用程序没有其他方法可发现它时，此信息对应用程序特别有用，例如，使用应用程序不知道的参数执行即席查询时。  
  
 应用程序通过使用 SQL_ATTR_AUTO_IPD 的*属性*调用**SQLGetConnectAttr**来确定驱动程序是否支持自动填充。 如果返回 SQL_TRUE，则驱动程序支持该驱动程序，并且应用程序可以通过将 SQL_ATTR_ENABLE_AUTO_IPD 语句特性设置为 SQL_TRUE 来启用它。  
  
 当支持并启用自动填充时，驱动程序将在包含参数标记的 SQL 语句已通过调用**SQLPrepare**准备好后填充 IPD 的字段。 应用程序可以通过调用**SQLGetDescField**或**SQLGetDescRec**或**SQLDescribeParam**检索此信息。 应用程序可以使用这些信息来绑定参数的最合适应用程序缓冲区，或为其指定数据转换。  
  
 自动填充 IPD 可能会导致性能下降。 应用程序可以通过将 SQL_ATTR_ENABLE_AUTO_IPD 语句特性重置为 SQL_FALSE （默认值）来关闭它。
