---
title: 描述符 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2138a5f8417fc9156c916719e96d707b9a29de9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040008"
---
# <a name="descriptors"></a>描述符
描述符句柄是指保存有关列或动态参数的信息的数据结构。  
  
 ODBC 函数进行隐式操作的列和参数数据设置和检索描述符字段。 例如，当**SQLBindCol**调用以将列数据绑定，它设置完整地描述绑定的描述符字段。 当**SQLColAttribute**调用来描述列的数据，它将返回描述符字段中存储数据。  
  
 调用 ODBC 函数的应用程序需要不考虑如何描述符。 没有数据库操作所需应用程序获取对描述符的直接访问权限。 但是，对于某些应用程序，直接访问描述符简化了许多操作。 例如，将定向到描述符的访问权限使您能够重新绑定列数据，可以是相对于调用更高效**SQLBindCol**试。  
  
> [!NOTE]  
>  未定义描述符的物理表示形式。 应用程序直接访问说明符仅通过其字段操作通过调用 ODBC 函数与描述符句柄。  
  
 本部分包含以下主题。  
  
-   [描述符类型](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [描述符字段](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [分配和释放描述符](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [获取和设置描述符字段](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
