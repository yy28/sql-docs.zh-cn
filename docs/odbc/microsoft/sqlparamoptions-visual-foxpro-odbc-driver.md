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
manager: craigg
ms.openlocfilehash: a66f0cd3a17baa9a09a5eeef2ade3d730f0a206b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806075"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别 1  
  
 允许应用程序指定的分配的参数集的多个值[SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)。 指定一组参数的多个值的功能可用于大容量插入和其他需要处理多个时间使用不同的参数值相同的 SQL 语句的数据源的工作。 例如，应用程序可以指定三组与关联的参数集值**插入**语句，然后执行**插入**语句一次执行了这三个插入操作。  
  
 有关详细信息，请参阅[SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md)中*ODBC 程序员参考*。
