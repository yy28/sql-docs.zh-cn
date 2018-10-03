---
title: SQLGetConnectOption （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5703eb39-f3b2-4f3a-8676-a5625ae29a41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62f1033abeaa32499602534f7f43b17fefe55ce9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767255"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 部分  
  
 ODBC API 一致性： 级别 1  
  
 返回一个连接选项的当前设置。 此函数支持部分： 驱动程序支持的所有值*fOption*自变量，但不支持的一些*vParam*值*fOption*参数SQL_TXN_ISOLATION。  
  
 下表描述了仅特定于 Visual FoxPro ODBC 驱动程序实现的行为与这些参数**SQLGetConnectOption**。  
  
|*fOption*|备注|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|如果您选择 SQL_AUTOCOMMIT_OFF，你的应用程序必须显式提交或回滚的事务[SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); Visual FoxPro ODBC 驱动程序不会自动提交完成后的事务语句。 如果语句是事务，该驱动程序才开始事务。|  
|SQL_CURRENT_QUALIFIER|可以是完全限定的数据库 （.dbc 文件） 名称或包含零个或多个表 （.dbf 文件） 的目录的完全限定的路径。|  
|SQL_LOGINTIMEOUT|返回"驱动程序不支持"错误。|  
|SQL_CURSORS|返回"驱动程序不支持"错误。|  
|SQL_PACKET_SIZE|返回"驱动程序不支持"错误。|  
|SQL_TXN_ISOLATION|驱动程序允许仅 SQL_TXN_READ_COMMITTED。<br /><br /> 以下*vParam*s 不支持：<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 有关详细信息，请参阅[SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md)中*ODBC 程序员参考*。
