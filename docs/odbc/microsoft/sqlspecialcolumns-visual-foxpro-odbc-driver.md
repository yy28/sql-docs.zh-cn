---
description: SQLSpecialColumns（Visual FoxPro ODBC 驱动程序）
title: SQLSpecialColumns (Visual FoxPro ODBC 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e83568c8370b56decb7c3f7c90cda443b88a72a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421601"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：级别1  
  
 检索唯一标识表中的行的一组最佳列。  
  
 Visual FoxPro ODBC 驱动程序返回组成 FoxPro 表中的主键的列。  (请参阅 [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)) 。如果在 *fColType* 设置为 SQL_ROWVER 的情况下调用，则不会返回列。 **SQLSpecialColumns** 仅适用于作为 [数据库](../../odbc/microsoft/visual-foxpro-terminology.md)的数据源。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) 。
