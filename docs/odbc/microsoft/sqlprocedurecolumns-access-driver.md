---
title: SQLProcedureColumns （Access 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a438823d1aa71eecb25c4935026c1b43e45842d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62637383"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns（Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 应用程序开发人员应查找驱动程序定义的列从结果集的末尾处开始并向后继续。  
  
|“列”|注释|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT 或 SQL_RESULT_COL|  
|序号|这是返回的结果集末尾的驱动程序特定列。 列的 SQL 类型是一个整数。|
