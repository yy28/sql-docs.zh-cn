---
title: 描述符 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8362a8dd210579ebca0d303ca29661a3774ea4cd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="descriptors"></a>描述符
描述符句柄是指保存有关列或动态参数的信息的数据结构。  
  
 ODBC 函数进行隐式操作的列和参数数据设置和检索描述符字段。 例如，当**SQLBindCol**称为将列数据绑定，它可以设置完整地描述绑定的描述符字段。 当**SQLColAttribute**调用来描述列的数据，它将返回描述符字段中存储的数据。  
  
 调用 ODBC 函数的应用程序不需要考虑本身具有描述符。 没有数据库操作需要应用程序获取直接访问描述符。 但是，对于某些应用程序，直接访问描述符，从而简化了许多操作。 例如，将向描述符访问使您能够重新绑定的列数据，其中可能更有效于调用**SQLBindCol**试。  
  
> [!NOTE]  
>  未定义的物理表示形式描述符。 应用程序获取只能由操作调用的描述符句柄与 ODBC 函数，其字段的直接访问属性的描述符。  
  
 本部分包含以下主题。  
  
-   [描述符类型](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [描述符字段](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [分配和释放描述符](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [获取和设置描述符字段](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
