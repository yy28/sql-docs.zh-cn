---
title: 绑定描述符记录 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 155ef4951abddc7a73d9d4abfbc45248f33d653c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306304"
---
# <a name="bound-descriptor-records"></a>绑定描述符记录
当应用程序设置描述符记录的SQL_DESC_DATA_PTR字段，使其不再包含 null 值时，该记录即表示为*绑定*。  
  
 如果描述符是 APD，则每个绑定记录构成绑定参数。 对于输入参数，应用程序在执行 语句之前必须为 SQL 语句中的每个动态参数标记绑定参数。 对于输出参数，应用程序不需要绑定该参数。  
  
 如果描述符是描述一行数据库数据的 ARD，则每个绑定记录构成一个绑定列。
