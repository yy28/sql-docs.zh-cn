---
title: "SQLSetConfigMode 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8919f758c486e6569b9620fcaa7bcf76f4dac0f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 函数
**一致性**  
 版本引入了： ODBC 3.0  
  
 **摘要**  
 **SQLSetConfigMode**设置配置模式下，该值指示系统信息中列出 DSN 值 Odbc.ini 该项，则其中。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>参数  
 *wConfigMode*  
 [输入]安装程序配置模式 （请参阅"备注"）。 中的值*wConfigMode*可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetConfigMode**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|无效的参数序列|*WConfigMode* ODBC_USER_DSN、 ODBC_SYSTEM_DSN 或 ODBC_BOTH_DSN 不包含自变量。|  
  
## <a name="comments"></a>注释  
 此函数用于设置中的系统信息列出 DSN 值 Odbc.ini 该项，则其中。 如果*wConfigMode* ODBC_USER_DSN，DSN 为用户 DSN，此函数将读取从中 HKEY_CURRENT_USER 的 Odbc.ini 条目。 如果它是 ODBC_SYSTEM_DSN，DSN 是系统 DSN 和此函数将读取从中 HKEY_LOCAL_MACHINE 的 Odbc.ini 条目。 如果它是 ODBC_BOTH_DSN，尝试 HKEY_CURRENT_USER，因而如果失败，则会使用 HKEY_LOCAL_MACHINE。  
  
 此函数不会影响**SQLCreateDataSource**和**SQLDriverConnect**。 将配置模式必须从注册表读取通过调用的驱动程序时，设置**SQLGetPrivateProfileString**或通过调用写入注册表**SQLWritePrivateProfileString**。 调用**SQLGetPrivateProfileString**和**SQLWritePrivateProfileString**使用将配置模式来了解哪些部分注册表上进行操作。  
  
> [!CAUTION]  
>  **SQLSetConfigMode**应调用仅根据需要; 如果不正确设置模式，ODBC 安装程序可能无法正常工作。  
  
 **SQLSetConfigMode**进行配置模式注册表直接修改。 这是除了通过调用修改配置模式的过程**SQLConfigDataSource**。 调用**SQLConfigDataSource**设置配置模式来修改 DSN 时区分用户和系统 Dsn。 在返回前, **SQLConfigDataSource**将配置模式下重置为 BOTHDSN。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|创建数据源|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|连接到使用连接字符串或对话框中的数据源|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|检索配置模式|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|

