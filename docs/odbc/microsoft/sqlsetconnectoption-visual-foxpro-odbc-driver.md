---
title: SQLSetConnectOption（可视化狐狸Pro ODBC驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2af208663f1e91250faad0ca9538b76bcec43b06
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301498"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持：部分  
  
 ODBC API 符合性：1 级  
  
 设置控制连接方面的选项。 此函数部分支持：驱动程序支持*fOption*参数的所有值，但不支持*fOption*参数SQL_TXN_ISOLATION的某些*vParam*值。  
  
 下表仅描述具有特定于**SQLSetConnectOption**的 Visual FoxPro ODBC 驱动程序实现的参数。  
  
|*fOption*|备注|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|如果选择SQL_AUTOCOMMIT_OFF，则应用程序必须显式提交或回滚[SQLTransact 的](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)事务。Visual FoxPro ODBC 驱动程序在完成时不会自动提交可交易声明。 如果语句是可操作的，则驱动程序确实会启动事务。|  
|SQL_CURRENT_QUALIFIER|可以是完全限定[的数据库](../../odbc/microsoft/visual-foxpro-terminology.md)名称或包含零个或多个[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录的完全限定路径。|  
|SQL_LOGINTIMEOUT|返回"驱动程序无法工作"错误。|  
|SQL_CURSORS|返回"驱动程序无法工作"错误。|  
|SQL_PACKET_SIZE|返回"驱动程序无法工作"错误。|  
|SQL_TXN_ISOLATION|驱动程序只允许SQL_TXN_READ_COMMITTED。<br /><br /> 不支持以下*vParams：*<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLSetConnectOption。](../../odbc/reference/syntax/sqlsetconnectoption-function.md)
