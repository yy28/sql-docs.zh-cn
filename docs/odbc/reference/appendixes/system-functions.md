---
title: 系统函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0c7817d37e14ad07b9cc64f59691c27cf665177
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070094"
---
# <a name="system-functions"></a>系统函数
下表列出了 ODBC 标量函数集中包含的系统函数。 通过调用**SQLGetInfo**与*信息类型*的 SQL_SYSTEM_FUNCTIONS，应用程序可以确定由驱动程序支持的系统函数。  
  
 参数表示为*exp*可以是名称的列中，结果的另一个标量函数或文本，其中基础数据类型可以表示为 SQL_NUMERIC、 SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL、 SQL_DOUBLE、 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 参数表示为*值*可以是文字常量，其中的基础数据类型可以表示为 SQL_NUMERIC、 SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL、 SQL_DOUBLE、 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 返回值表示为 ODBC 数据类型。  
  
|函数|描述|  
|--------------|-----------------|  
|**DATABASE( )**  (ODBC 1.0)|返回与连接句柄相对应的数据库的名称。 (数据库的名称中也有通过调用**SQLGetConnectOption** SQL_CURRENT_QUALIFIER 连接选项。)|  
|**IFNULL (** _exp_，_值_ **)** (ODBC 1.0)|如果*exp*为 null，*值*返回。 如果*exp*不为 null， *exp*返回。 可能的数据类型或类型的*值*必须是兼容的数据类型*exp*。|  
|**用户 （)** (ODBC 1.0)|返回在 DBMS 中的用户名称。 (用户名称也是可**SQLGetInfo**通过指定的信息类型：SQL_USER_NAME。)这可以是不同于登录名。|
