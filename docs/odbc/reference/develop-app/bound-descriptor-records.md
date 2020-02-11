---
title: 绑定描述符记录 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d0016a2849feb5656cb3cd6dd46eff444f37058
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118763"
---
# <a name="bound-descriptor-records"></a>绑定描述符记录
当应用程序设置描述符记录的 "SQL_DESC_DATA_PTR" 字段，使其不再包含 null 值时，将被称为 "*绑定*"。  
  
 如果描述符为 APD，则每个绑定记录都构成一个绑定参数。 对于输入参数，应用程序必须在执行语句前为 SQL 语句中的每个动态参数标记绑定一个参数。 对于输出参数，应用程序不需要绑定参数。  
  
 如果描述符是描述数据库数据行的 ARD，则每个绑定记录构成一个绑定列。
