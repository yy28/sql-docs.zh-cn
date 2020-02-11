---
title: SQLSetConnectOption （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 48a4c8666ab7aa7e210289564210d99c947e5631
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071715"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：部分  
  
 ODBC API 一致性：级别1  
  
 设置控制连接各个方面的选项。 此函数部分受支持：驱动程序支持*fOption*参数的所有值，但不支持*fOption*参数 SQL_TXN_ISOLATION 的某些*vParam*值。  
  
 下表仅介绍了特定于**SQLSetConnectOption**的 VISUAL FoxPro ODBC 驱动程序实现的行为的参数。  
  
|*fOption*|备注|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|如果选择 SQL_AUTOCOMMIT_OFF，应用程序必须通过[SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)显式提交或回滚事务。Visual FoxPro ODBC 驱动程序不会在完成时自动提交事务语句。 如果语句为事务，则驱动程序将开始事务。|  
|SQL_CURRENT_QUALIFIER|可以是完全限定的[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)名称，也可以是包含零个或多个[自由表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录的完全限定路径。|  
|SQL_LOGINTIMEOUT|返回 "驱动程序不支持" 错误。|  
|SQL_CURSORS|返回 "驱动程序不支持" 错误。|  
|SQL_PACKET_SIZE|返回 "驱动程序不支持" 错误。|  
|SQL_TXN_ISOLATION|驱动程序仅允许 SQL_TXN_READ_COMMITTED。<br /><br /> 不支持以下*vParam*：<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) 。
