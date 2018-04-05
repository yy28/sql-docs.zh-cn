---
title: SQLSetConnectOption （Visual FoxPro ODBC 驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4667e8c80c183cb22b7199e2f404ca5eb79c5c5c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 部分  
  
 ODBC API 一致性： 级别 1  
  
 设置控制方面的连接的选项。 此函数支持部分： 驱动程序支持的所有值*fOption*自变量，但不支持的某些*vParam*值*fOption*自变量SQL_TXN_ISOLATION。  
  
 下表描述仅与特定于 Visual FoxPro ODBC 驱动程序实现的行为的这些自变量**SQLSetConnectOption**。  
  
|*fOption*|Remarks|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|如果你选择 SQL_AUTOCOMMIT_OFF，你的应用程序必须显式提交或回滚的事务[SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); Visual FoxPro ODBC 驱动程序不会自动提交完成后的 transactable 语句。 如果语句是 transactable，驱动程序才开始事务。|  
|SQL_CURRENT_QUALIFIER|可以是完全限定[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)名称或完全限定的路径的目录包含零个或多个[释放表](../../odbc/microsoft/visual-foxpro-terminology.md)。|  
|SQL_LOGINTIMEOUT|返回"驱动程序不支持"错误。|  
|SQL_CURSORS|返回"驱动程序不支持"错误。|  
|SQL_PACKET_SIZE|返回"驱动程序不支持"错误。|  
|SQL_TXN_ISOLATION|驱动程序允许仅 SQL_TXN_READ_COMMITTED。<br /><br /> 以下*vParam*s 不支持：<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 有关详细信息，请参阅[SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md)中*ODBC 程序员参考*。
