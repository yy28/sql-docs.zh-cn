---
title: 如何使用元数据？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbbba96fa2e99a2ccc0618f31e3b29e7d479f703
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300167"
---
# <a name="how-is-metadata-used"></a>如何使用元数据？
应用程序需要大多数结果集操作的元数据。 例如，应用程序使用某列的数据类型来确定要将哪一种变量绑定到该列； 它使用字符列的字节长度来确定显示该列数据所需的空间。 应用程序确定列的元数据的方式取决于应用程序的类型。  
  
 垂直应用程序使用预定义的表，并对这些表执行预定义的操作。 由于此类应用程序的结果集元数据是在应用程序编写之前定义的，并且由应用程序开发人员控制，因此可以硬编码到应用程序中。 例如，如果在数据源中将顺序 ID 列定义为 4 字节整数，则应用程序可以始终将 4 字节整数绑定到该列。 如果元数据在应用程序中为硬编码，则对应用程序所用的表进行更改通常意味着要对应用程序代码进行更改。 这很少是一个问题，因为此类更改通常是作为应用程序的新版本的一部分进行的。  
  
 与垂直应用程序一样，自定义应用程序通常使用预定义的表，并在这些表上执行预定义的操作。 例如，可以编写应用程序来在三个不同的数据源之间传输数据;写入应用程序时，通常知道要传输的数据。 因此，自定义应用程序也往往具有硬编码的元数据。  
  
 通用应用程序（尤其是支持临时查询的应用程序）几乎永远不会知道它们创建的结果集的元数据。 因此，他们必须使用**SQLNumResultCols、SQLDescribeCol**和**SQLColAttribute**等函数在运行时发现元数据，下一节将介绍[SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)。 **SQLDescribeCol**  
  
 所有应用程序（无论其类型如何）都可以对目录函数返回的结果集的元数据进行硬编码。 这些结果集在本手册的参考部分中定义。
