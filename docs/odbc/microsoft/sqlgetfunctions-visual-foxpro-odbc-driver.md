---
title: SQLGetFunctions （Visual FoxPro ODBC 驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8102932a-88b3-49d8-bf7a-c766f54878c0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc3350e8b6a7a4ddcf505fed14a056422cbbbe41
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904772"
---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别 1  
  
 返回适用于所有支持的函数。  
  
 Visual FoxPro ODBC 驱动程序还支持所有 ODBC API 核心和级别 1 的函数。 下表指示驱动程序是否支持特定的级别 2 函数。  
  
|*函数*|Supported|  
|----------------|---------------|  
|SQL_API_SQLBROWSECONNECT|否|  
|SQL_API_SQLCOLUMNPRIVELEGES|否|  
|SQL_API_SQLDATASOURCES|是|  
|SQL_API_SQLDESCRIBEPARAM|否|  
|SQL_API_SQLDRIVERS|是|  
|SQL_API_SQLEXTENDEDFETCH|是|  
|SQL_API_SQLFOREIGNKEYS|否|  
|SQL_API_SQLMORERESULTS|是|  
|SQL_API_SQLNATIVESQL|否|  
|SQL_API_SQLNUMPARAMS|是|  
|SQL_API_SQLPARAMOPTIONS|是|  
|SQL_API_SQLPRIMARYKEYS|是|  
|SQL_API_SQLPROCEDURECOLUMNS|否|  
|SQL_API_SQLPROCEDURES|否|  
|SQL_API_SQLSETPOS|是|  
|SQL_API_SQLSETSCROLLOPTIONS|是|  
|SQL_API_SQLTABLEPRIVILEGES|否|  
  
 有关详细信息，请参阅[SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md)中*ODBC 程序员参考*。
