---
title: 是如何使用元数据？ | Microsoft Docs
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
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c4779c5e60b97a389ebf686678c9a989fb933cb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="how-is-metadata-used"></a>是如何使用元数据？
应用程序需要大多数结果集操作的元数据。 例如，应用程序使用某列的数据类型来确定要将哪一种变量绑定到该列； 它使用的字节长度的字符列来确定需要显示该列中的数据的空间量。 应用程序确定列的元数据的方式取决于应用程序的类型。  
  
 垂直应用程序处理的预定义的表和执行在这些表上的预定义的操作。 因为此类应用程序的结果集元数据定义应用程序甚至编写，并由应用程序开发人员控制之前，它可以是硬编码到应用程序。 例如，如果在数据源中将顺序 ID 列定义为 4 字节整数，则应用程序可以始终将 4 字节整数绑定到该列。 如果元数据在应用程序中为硬编码，则对应用程序所用的表进行更改通常意味着要对应用程序代码进行更改。 这是很少出现问题，因为通常作为应用程序的新版本的一部分进行这样的更改。  
  
 类似于垂直应用程序，自定义应用程序通常使用预定义的表并执行在这些表上的预定义的操作。 例如，可能会写入应用程序以三种不同的数据源; 之间传输数据要传输的数据通常称为编写应用程序。 因此，自定义应用程序还往往采用硬编码的元数据。  
  
 通用应用程序，尤其是那些支持即席查询，几乎从未知道他们创建的结果集的元数据。 因此，它们必须在运行时使用函数发现元数据**SQLNumResultCols**， **SQLDescribeCol**，和**SQLColAttribute**中, 描述这些下一部分中， [SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)。  
  
 所有应用程序，而不考虑其类型，可以通过目录函数返回的结果集的硬编码元数据。 在此手册的参考部分中定义这些结果集。
