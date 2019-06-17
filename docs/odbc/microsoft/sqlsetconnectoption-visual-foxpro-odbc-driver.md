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
manager: craigg
ms.openlocfilehash: 398d098615a0453cb016286867836388fd817540
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63473030"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：Partial  
  
 ODBC API 一致性：级别 1  
  
 设置可以控制以下方面的连接的选项。 部分支持此函数：该驱动程序支持的所有值*fOption*自变量，但不支持的一些*vParam*值*fOption* SQL_TXN_ISOLATION 参数。  
  
 下表描述了仅特定于 Visual FoxPro ODBC 驱动程序实现的行为与这些参数**SQLSetConnectOption**。  
  
|*fOption*|备注|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|如果您选择 SQL_AUTOCOMMIT_OFF，你的应用程序必须显式提交或回滚的事务[SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); Visual FoxPro ODBC 驱动程序不会自动提交完成后的事务语句。 如果语句是事务，该驱动程序才开始事务。|  
|SQL_CURRENT_QUALIFIER|可以是完全限定[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)名称或完全限定的路径到一个目录，其中包含零个或多个[免费表](../../odbc/microsoft/visual-foxpro-terminology.md)。|  
|SQL_LOGINTIMEOUT|返回"驱动程序不可用"错误。|  
|SQL_CURSORS|返回"驱动程序不可用"错误。|  
|SQL_PACKET_SIZE|返回"驱动程序不可用"错误。|  
|SQL_TXN_ISOLATION|驱动程序允许仅 SQL_TXN_READ_COMMITTED。<br /><br /> 以下*vParam*s 不支持：<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 有关详细信息，请参阅[SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md)中*ODBC 程序员参考*。
