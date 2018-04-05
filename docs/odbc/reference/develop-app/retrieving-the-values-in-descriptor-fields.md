---
title: 检索描述符字段中的值 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 37efd70ccd8fa0ad5c6d4bb573eb1c158a3ec35b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>检索描述符字段中的值
应用程序可以调用**SQLGetDescField**以获取单个字段的描述符记录。 **SQLGetDescField**向 ODBC 中, 定义的所有描述符字段和驱动程序定义的字段以及提供应用程序访问。  
  
 **SQLGetDescRec**可以调用以进行检索的设置会影响的数据类型的多个描述符字段和列或参数的数据的存储。
