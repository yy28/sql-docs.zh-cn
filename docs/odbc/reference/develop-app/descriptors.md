---
description: 描述符
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae01f093ef1b67f1326f8aa7719b74100fcba462
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429329"
---
# <a name="descriptors"></a>描述符
描述符句柄指保存有关列或动态参数的信息的数据结构。  
  
 对列和参数数据进行隐式设置并检索描述符字段的 ODBC 函数。 例如，当调用 **SQLBindCol** 绑定列数据时，它会设置完全描述绑定的描述符字段。 当调用 **SQLColAttribute** 来描述列数据时，它将返回存储在描述符字段中的数据。  
  
 调用 ODBC 函数的应用程序无需考虑到描述符。 无数据库操作要求应用程序获得对描述符的直接访问权限。 但对于某些应用程序，获取对描述符的直接访问可以简化许多操作。 例如，直接访问描述符可提供一种重新绑定列数据的方法，这比再次调用 **SQLBindCol** 更有效。  
  
> [!NOTE]  
>  描述符的物理表示形式未定义。 应用程序通过使用描述符句柄调用 ODBC 函数，仅获取对描述符的直接访问。  
  
 本部分包含以下主题。  
  
-   [描述符类型](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [描述符字段](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [分配和释放描述符](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [获取和设置描述符字段](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
