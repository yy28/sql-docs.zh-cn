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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909831"
---
# <a name="automatic-population-of-the-ipd"></a>自动填充 IPD
某些驱动程序都能参数化的查询已准备好后设置 IPD 的字段。 有关参数，包括数据类型、 精度、 小数位数和其他特征的信息自动填充的描述符字段。 这相当于支持**SQLDescribeParam**。 具有其他方式来发现它，例如使用应用程序不知道的参数执行即席查询的时间时，此信息可以是特别有价值的应用程序。  
  
 应用程序确定驱动程序是否支持自动填充通过调用**SQLGetConnectAttr**与*属性*SQL_ATTR_AUTO_IPD。 如果返回 SQL_TRUE，则驱动程序支持它并且应用程序可以通过将 SQL_ATTR_ENABLE_AUTO_IPD 语句属性设置为 SQL_TRUE 启用它。  
  
 包含参数标记的 SQL 语句已准备好通过调用后，该驱动程序时支持和启用自动填充，填充 IPD 的字段**SQLPrepare**。 应用程序可以检索此信息通过调用**SQLGetDescField**或**SQLGetDescRec**，或**SQLDescribeParam**。 应用程序可以使用信息，以将为参数最合适的应用程序缓冲区绑定或为其指定的数据转换。  
  
 自动填充 IPD 可能会产生对性能产生负面影响。 应用程序可以将其关闭由正在 SQL_ATTR_ENABLE_AUTO_IPD 语句属性重置为 SQL_FALSE （默认值）。
