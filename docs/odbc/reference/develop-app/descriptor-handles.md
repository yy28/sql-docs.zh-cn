---
title: "描述符句柄 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44f8593c55579c40854190c8710fdfde0b753d0a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="descriptor-handles"></a>描述符句柄
A*描述符*是描述 SQL 语句的参数或结果集的列的元数据的集合，如所示的应用程序或驱动程序 (也称为*实现*)。 因此，描述符可填充所有四个角色：  
  
-   **应用程序参数描述符 (APD)。** 包含有关绑定到在 SQL 语句中，如其地址、 长度和 C 数据类型参数的应用程序缓冲区的信息。  
  
-   **实现参数描述符 (IPD)。** 包含有关在 SQL 语句中，如其 SQL 数据类型、 长度和可为 null 的参数信息。  
  
-   **应用程序行描述符 (ARD)。** 包含有关绑定到结果集中，例如其地址、 长度和 C 数据类型的列的应用程序缓冲区的信息。  
  
-   **实现行描述符 (IRD)。** 包含有关中的结果集，如其 SQL 数据类型、 长度和可为 null 的列信息。  
  
 在分配一个语句时，将自动分配 （一个填充每个角色） 的四个描述符。 这些被称为*自动分配描述符*并且始终与该语句相关联。 应用程序还可以将分配与描述符**SQLAllocHandle**。 这些被称为*显式分配描述符*。 它们在连接上分配，以及可以与该连接以满足 APD 或 ARD 的这些语句上的角色上的一个或多个语句相关联。  
  
 ODBC 中的大多数操作可以由应用程序执行无需显式使用描述符。 但是，描述符对于某些操作提供的方便快捷方式。 例如，假设应用程序要将数据从两组不同的缓冲区。 若要使用的缓冲区的第一组，它重复应该调用**SQLBindParameter**以将其绑定到中的参数**插入**语句，然后执行该语句。 若要使用的缓冲区的第二个集，它将重复此过程。 或者，它无法设置绑定到一个描述符中的缓冲区的第一个集和第二个集的另一个描述符中的缓冲区。 若要切换的绑定的集，应用程序将只调用**SQLSetStmtAttr**并作为 APD 语句关联的正确的描述符。  
  
 有关描述符的详细信息，请参阅[类型的描述符](../../../odbc/reference/develop-app/types-of-descriptors.md)。
