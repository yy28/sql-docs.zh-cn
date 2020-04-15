---
title: IPD 的自动填充 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1998ea1992ee7f14d87d01e348d955b017166088
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285067"
---
# <a name="automatic-population-of-the-ipd"></a>自动填充 IPD
在准备好参数化查询后，某些驱动程序能够设置 IPD 的字段。 描述符字段会自动填充有关参数的信息，包括数据类型、精度、比例和其他特征。 这相当于支持**SQLDescribeParam。** 当应用程序没有其他方法发现此信息时，例如使用应用程序不知道的参数执行临时查询时，此信息对于应用程序来说可能特别有价值。  
  
 应用程序通过调用具有SQL_ATTR_AUTO_IPD*属性*的**SQLGetConnectAttr**来确定驱动程序是否支持自动填充。 如果返回SQL_TRUE，驱动程序将支持它，应用程序可以通过将SQL_ATTR_ENABLE_AUTO_IPD语句属性设置为SQL_TRUE来启用它。  
  
 支持并启用自动填充后，驱动程序在 SQL 语句通过调用**SQLPrepare**编写后填充 IPD 的字段。 应用程序可以通过调用**SQLGetDescField**或**SQLGetDescRec**或**SQLDescribeParam**来检索此信息。 应用程序可以使用信息绑定参数最适当的应用程序缓冲区，或为其指定数据转换。  
  
 IPD 的自动填充可能会产生性能损失。 应用程序可以通过将SQL_ATTR_ENABLE_AUTO_IPD语句属性重置为SQL_FALSE（默认值）来将其关闭。
