---
title: SQLParamOptions （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1adbde1b3df38d2b602f1ec42a2c96f36e8bd67b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996374"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：级别1  
  
 允许应用程序为[SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)分配的参数集指定多个值。 为一组参数指定多个值的功能对于大容量插入和其他需要数据源使用各种参数值多次处理同一 SQL 语句的工作非常有用。 例如，应用程序可以为与**INSERT**语句关联的参数集指定三组值，然后执行**insert**语句一次来执行三个插入操作。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) 。
