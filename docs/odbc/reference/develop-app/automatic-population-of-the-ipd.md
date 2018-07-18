---
title: 自动填充的 IPD |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9e3d80ea280e4487f5443bca8152a3a541dfbd8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908352"
---
# <a name="automatic-population-of-the-ipd"></a>自动填充的 IPD
某些驱动程序都能准备好参数化的查询之后设置 IPD 的字段。 描述符字段自动填充有关参数，包括数据类型、 精度、 小数位数和其他特征的信息。 这相当于支持**SQLDescribeParam**。 它还没有发现它，例如当应用程序不知道的参数以进行即席查询时的其他方法时，此信息可能特别有价值的应用程序。  
  
 应用程序确定的驱动程序是否通过调用支持自动填充**SQLGetConnectAttr**与*属性*SQL_ATTR_AUTO_IPD。 如果返回 SQL_TRUE，驱动程序支持它，应用程序可以通过将 SQL_ATTR_ENABLE_AUTO_IPD 语句属性设置为 SQL_TRUE 启用它。  
  
 支持并启用自动填充程序，该驱动程序将填充的字段的 IPD 包含参数标记的 SQL 语句已准备好通过调用之后**SQLPrepare**。 应用程序可以通过调用来检索此信息**SQLGetDescField**或**SQLGetDescRec**，或**SQLDescribeParam**。 若要将绑定参数的最适合应用程序缓冲区，或若要为其指定的数据转换，应用程序可以使用信息。  
  
 自动填充的 IPD 可能会产生对性能产生负面影响。 应用程序可以将其关闭由正在 SQL_ATTR_ENABLE_AUTO_IPD 语句属性重置为 SQL_FALSE （默认值）。
