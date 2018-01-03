---
title: "绑定描述符记录 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 21074ecc6e606b3b235f4eb32bc1f1911136d335
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="bound-descriptor-records"></a>绑定描述符记录
当应用程序设置的描述符记录 SQL_DESC_DATA_PTR 字段，以使其不再包含 null 值时，该记录称为*绑定*。  
  
 如果该描述符不 APD，每个绑定的记录会产生绑定的参数。 用于输入参数，应用程序必须将每个动态参数标记的参数绑定之前执行的语句的 SQL 语句中。 对于输出参数，应用程序需要将该参数未绑定。  
  
 如果该描述符不 ARD，其中介绍了数据库数据行，每个绑定的记录会产生绑定的列。
