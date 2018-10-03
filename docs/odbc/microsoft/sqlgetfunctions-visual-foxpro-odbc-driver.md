---
title: SQLGetFunctions （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8102932a-88b3-49d8-bf7a-c766f54878c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0ae7b8eb0468dd401009ef58c83b87606b0679a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628604"
---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别 1  
  
 返回支持的所有函数，则返回 TRUE。  
  
 Visual FoxPro ODBC 驱动程序支持所有 ODBC API 核心和 1 级函数。 下表指示驱动程序是否支持特定的级别 2 函数。  
  
|*函数*|是否支持|  
|----------------|---------------|  
|SQL_API_SQLBROWSECONNECT|否|  
|SQL_API_SQLCOLUMNPRIVELEGES|否|  
|SQL_API_SQLDATASOURCES|用户帐户控制|  
|SQL_API_SQLDESCRIBEPARAM|否|  
|SQL_API_SQLDRIVERS|用户帐户控制|  
|SQL_API_SQLEXTENDEDFETCH|用户帐户控制|  
|SQL_API_SQLFOREIGNKEYS|否|  
|SQL_API_SQLMORERESULTS|用户帐户控制|  
|SQL_API_SQLNATIVESQL|否|  
|SQL_API_SQLNUMPARAMS|用户帐户控制|  
|SQL_API_SQLPARAMOPTIONS|用户帐户控制|  
|SQL_API_SQLPRIMARYKEYS|用户帐户控制|  
|SQL_API_SQLPROCEDURECOLUMNS|否|  
|SQL_API_SQLPROCEDURES|否|  
|SQL_API_SQLSETPOS|用户帐户控制|  
|SQL_API_SQLSETSCROLLOPTIONS|用户帐户控制|  
|SQL_API_SQLTABLEPRIVILEGES|否|  
  
 有关详细信息，请参阅[SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md)中*ODBC 程序员参考*。
