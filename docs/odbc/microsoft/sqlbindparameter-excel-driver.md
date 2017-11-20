---
title: "SQLBindParameter （Excel 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Excel driver [ODBC], SQLBindParameter
- SQLBindParameter function [ODBC], Excel Driver
ms.assetid: 40489bc5-3e2a-425e-892d-e0dc037f4d7a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 013f19579815dfcac2fcfe78cbbe41919bff9c15
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindparameter-excel-driver"></a>SQLBindParameter （Excel 驱动程序）
> [!NOTE]  
>  本主题提供 Excel 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 当使用 Microsoft Excel 驱动程序时，执行 INSERT 语句使用的参数将 NULL 插入 SQL_CHAR 列将返回 SQL_SUCCESS_WITH_INFO 与 SQLSTATE 01004，"数据截断。"

