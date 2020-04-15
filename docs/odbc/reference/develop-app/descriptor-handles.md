---
title: 描述符句柄 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed0595c97f3f4ad92d976c89327a01e25cb5b753
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305908"
---
# <a name="descriptor-handles"></a>描述符句柄
*描述符*是一组元数据，用于描述 SQL 语句的参数或结果集的列，如应用程序或驱动程序（也称为*实现*）所示。 因此，描述符可以填充四个角色中的任何一个：  
  
-   **应用程序参数描述符 （APD）。** 包含有关绑定到 SQL 语句中参数的应用程序缓冲区的信息，例如其地址、长度和 C 数据类型。  
  
-   **实现参数描述符 （IPD）。** 包含有关 SQL 语句中参数的信息，例如其 SQL 数据类型、长度和空值。  
  
-   **应用程序行描述符 （ARD）。** 包含有关绑定到结果集中列的应用程序缓冲区的信息，例如其地址、长度和 C 数据类型。  
  
-   **实现行描述符 （IRD）。** 包含有关结果集中列的信息，例如其 SQL 数据类型、长度和空值。  
  
 分配语句时，将自动分配四个描述符（每个角色一个填充）。 这些称为*自动分配的描述符*，并且始终与该语句相关联。 应用程序还可以使用**SQLAllocHandle**分配描述符。 这些被称为*显式分配的描述符*。 它们在连接上分配，并可以与该连接上的一个或多个语句相关联，以履行 APD 或 ARD 在这些语句上的作用。  
  
 ODBC 中的大多数操作都可以执行，而无需应用程序显式使用描述符。 但是，描述符为某些操作提供了方便的快捷方式。 例如，假设应用程序希望插入来自两组不同缓冲区的数据。 若要使用第一组缓冲区，它将重复调用**SQLBindparameter**将它们绑定到**INSERT**语句中的参数，然后执行该语句。 要使用第二组缓冲区，它将重复此过程。 或者，它可以在一个描述符中设置对第一组缓冲区的绑定，在另一个描述符中设置第二组缓冲区的绑定。 要在绑定集之间切换，应用程序只需调用**SQLSetStmtAttr**并将正确的描述符与语句关联为 APD。  
  
 有关描述符的详细信息，请参阅[描述符的类型](../../../odbc/reference/develop-app/types-of-descriptors.md)。
