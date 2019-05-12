---
title: SQLSetConfigMode 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b40da961e3e659bf4cd3e3692b4674399bce47a6
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537216"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 函数
**符合性**  
 版本引入了：ODBC 3.0  
  
 **摘要**  
 **SQLSetConfigMode**设置指示列出 DSN 的值的 Odbc.ini 项所在的系统信息中的配置模式。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>参数  
 *wConfigMode*  
 [输入]安装程序配置模式 （请参阅"注释"）。 中的值*wConfigMode*可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetConfigMode**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|无效的参数序列|*WConfigMode* ODBC_USER_DSN、 ODBC_SYSTEM_DSN 或 ODBC_BOTH_DSN 不包含参数。|  
  
## <a name="comments"></a>注释  
 此函数用于设置其中列出 DSN 的值的 Odbc.ini 条目是在系统信息。 如果*wConfigMode* ODBC_USER_DSN，DSN 是一个用户 DSN 和此函数将读取从 HKEY_CURRENT_USER 中的 Odbc.ini 条目。 如果 ODBC_SYSTEM_DSN，DSN 是系统 DSN，此函数将读取从 HKEY_LOCAL_MACHINE 中的 Odbc.ini 条目。 如果它是 ODBC_BOTH_DSN，尝试 HKEY_CURRENT_USER，和如果失败，则会使用 HKEY_LOCAL_MACHINE。  
  
 此函数不会影响**SQLCreateDataSource**并**SQLDriverConnect**。 配置模式必须设置时驱动程序中通过调用从注册表读取**SQLGetPrivateProfileString**或通过调用写入注册表**SQLWritePrivateProfileString**。 调用**SQLGetPrivateProfileString**并**SQLWritePrivateProfileString**使用配置模式来了解注册表，以对哪个部分。  
  
> [!CAUTION]  
>  **SQLSetConfigMode**仅 ODBC 安装程序时必需的; 如果未正确设置模式，可能无法正常工作，应调用。  
  
 **SQLSetConfigMode**进行直接注册表修改的配置模式。 这是通过调用修改配置模式的过程除了**SQLConfigDataSource**。 调用**SQLConfigDataSource**设置配置模式来修改 DSN 时区分用户和系统 Dsn。 在返回前, **SQLConfigDataSource**将配置模式下重置为 BOTHDSN。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|创建数据源|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|连接到使用连接字符串或对话框中的数据源|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|检索配置模式|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
