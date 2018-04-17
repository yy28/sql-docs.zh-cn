---
title: SQLProcedureColumns （Access 驱动程序） |Microsoft 文档
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
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 59cb68c06193d081bede5ff9ad33b08adb4c8235
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns （Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 应用程序开发人员应查找驱动程序定义的列从结果集末尾处开始和向后继续。  
  
|列|注释|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT 或 SQL_RESULT_COL|  
|序号|这是特定于驱动程序返回列中的结果集末尾。 列的 SQL 类型是一个整数。|
