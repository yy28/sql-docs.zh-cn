---
title: SQL程序列（访问驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be17776ac6b6879140a7c57bede1b3cb539d97be
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299457"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 应用程序开发人员应查找从结果集末尾开始并向后移动的驱动程序定义的列。  
  
|列|注释|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT或SQL_RESULT_COL|  
|序|这是在结果集末尾返回的特定于驱动程序的列。 列的 SQL 类型是整数。|
