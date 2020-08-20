---
description: 如何使用元数据？
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
ms.openlocfilehash: ca61677b0001ba4c39f81f80f6e3cbce26f27910
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476629"
---
# <a name="how-is-metadata-used"></a>如何使用元数据？
应用程序需要大多数结果集操作的元数据。 例如，应用程序使用某列的数据类型来确定要将哪一种变量绑定到该列； 它使用字符列的字节长度来确定显示该列的数据所需的空间量。 应用程序确定列的元数据的方式取决于应用程序的类型。  
  
 垂直应用程序使用预定义的表，并对这些表执行预定义的操作。 由于此类应用程序的结果集元数据是在编写应用程序之前定义的，由应用程序开发人员控制的，因此，可以将其硬编码到应用程序中。 例如，如果在数据源中将顺序 ID 列定义为 4 字节整数，则应用程序可以始终将 4 字节整数绑定到该列。 如果元数据在应用程序中为硬编码，则对应用程序所用的表进行更改通常意味着要对应用程序代码进行更改。 这种情况很少出现问题，因为此类更改通常作为新版本的应用程序的一部分进行。  
  
 与垂直应用程序一样，自定义应用程序通常使用预定义的表，并对这些表执行预定义的操作。 例如，可以编写一个应用程序，以在三个不同的数据源之间传输数据;写入应用程序时通常会识别要传输的数据。 因此，自定义应用程序也倾向于使用硬编码的元数据。  
  
 一般的应用程序（尤其是支持即席查询的应用程序）几乎不知道它们所创建的结果集的元数据。 因此，它们必须在运行时使用函数 **SQLNumResultCols**、 **SQLDescribeCol**和 **SQLColAttribute**（在下一节 [SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)中介绍）发现元数据。  
  
 所有应用程序，无论其类型如何，都可以将目录函数返回的结果集的元数据硬编码。 这些结果集是在本手册的 "参考" 部分中定义的。
