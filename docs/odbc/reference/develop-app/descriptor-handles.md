---
title: 描述符句柄 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 24e3d4c87f3bc461a339a6cb635d64f20dc73e20
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106163"
---
# <a name="descriptor-handles"></a>描述符句柄
一个*描述符*显示的应用程序或驱动程序是一系列介绍了 SQL 语句的参数或结果集的列的元数据 (也称为*实现*)。 因此，一个描述符可以填充所有四个角色：  
  
-   **应用程序参数描述符 (APD)。** 包含有关应用程序缓冲区绑定到在 SQL 语句中，例如其地址、 长度和 C 数据类型的参数信息。  
  
-   **实现参数描述符 (IPD)。** 包含有关在 SQL 语句中，如其 SQL 数据类型、 长度和为 null 性的参数信息。  
  
-   **应用程序行描述符 (ARD)。** 包含有关应用程序缓冲区绑定到结果集中，例如其地址、 长度和 C 数据类型的列的信息。  
  
-   **实现行描述符 (IRD)。** 包含在结果集中，如其 SQL 数据类型、 长度和为 null 性的列信息。  
  
 分配一个语句时，将自动分配 （一个填充每个角色） 的四个描述符。 这些参数称为*自动分配的描述符*，都始终与该语句。 应用程序还可以分配与描述符**SQLAllocHandle**。 这些参数称为*显式分配描述符*。 它们将分配的连接，并且可以与该连接来满足这些语句的 APD 或 ARD 角色上的一个或多个语句相关联。  
  
 ODBC 中的大多数操作可以由应用程序执行而无需显式使用的描述符。 但是，描述符对于某些操作提供的方便的快捷方式。 例如，假设应用程序想要将数据从两组不同的缓冲区。 若要使用的缓冲区的第一个集，它反复将调用**SQLBindParameter**以将其绑定到中的参数**插入**语句，然后执行该语句。 若要使用的缓冲区的第二个集，它会重复此过程。 或者，它可以设置绑定到一个描述符中的缓冲区的第一个集和第二个组中其他描述符的缓冲区。 若要切换的绑定集之间，应用程序将只调用**SQLSetStmtAttr**并将正确的描述符与作为 APD 语句相关联。  
  
 有关描述符的详细信息，请参阅[类型的描述符](../../../odbc/reference/develop-app/types-of-descriptors.md)。
