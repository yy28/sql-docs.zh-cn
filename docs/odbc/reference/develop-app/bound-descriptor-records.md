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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118763"
---
# <a name="bound-descriptor-records"></a>绑定描述符记录
当应用程序，使其不再包含 null 值将设置 SQL_DESC_DATA_PTR 字段的描述符记录时，记录称*绑定*。  
  
 如果该描述符是 APD，每个绑定的记录构成绑定的参数。 用于输入参数，该应用程序必须将每个动态参数标记的参数绑定中执行该语句前的 SQL 语句。 对于输出参数，该应用程序需要将该参数未绑定。  
  
 如果该描述符是 ARD，其中介绍了数据库数据的行，每个绑定的记录构成了绑定的列。
