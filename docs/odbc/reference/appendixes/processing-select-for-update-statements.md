---
title: 处理 SELECT FOR UPDATE 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f54d31426773f294a4a23f059c9f906d430056f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721755"
---
# <a name="processing-select-for-update-statements"></a>处理 SELECT FOR UPDATE 语句
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 最大互操作性，应用程序应生成结果集将使用定位的 update 语句更新通过执行**选择更新**语句。 尽管游标库不需要它，但它需要支持定位的 update 语句的大多数数据源。  
  
 游标库会忽略中的列**FOR UPDATE**子句**SELECT FOR UPDATE**语句; 它将该语句传递给驱动程序之前删除此子句。 在游标库中，将 sql_attr_concurrency 设置语句属性，以及在上一节中所述的限制控件是否在结果中的列设置可以进行更新。
