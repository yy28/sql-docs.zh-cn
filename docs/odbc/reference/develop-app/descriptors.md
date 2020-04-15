---
title: 描述符 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca8299daae744fb9398ed6ffc99c838ce8edff48
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305898"
---
# <a name="descriptors"></a>描述符
描述符句柄是指保存有关列或动态参数的信息的数据结构。  
  
 ODBC 函数对列和参数数据进行隐式设置和检索描述符字段。 例如，当调用**SQLBindCol**来绑定列数据时，它会设置完全描述绑定的描述符字段。 当调用**SQLColAttribute**来描述列数据时，它将返回存储在描述符字段中的数据。  
  
 调用 ODBC 函数的应用程序不需要关注描述符本身。 没有数据库操作要求应用程序直接访问描述符。 但是，对于某些应用程序，直接访问描述符可以简化许多操作。 例如，直接访问描述符提供了重新绑定列数据的方法，这比再次调用**SQLBindCol**更有效。  
  
> [!NOTE]  
>  描述符的物理表示形式未定义。 应用程序只能通过使用描述符句柄调用 ODBC 函数来直接访问描述符。  
  
 本部分包含以下主题。  
  
-   [描述符类型](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [描述符字段](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [分配和释放描述符](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [获取和设置描述符字段](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
