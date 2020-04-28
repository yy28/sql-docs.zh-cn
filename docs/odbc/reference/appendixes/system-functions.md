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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca71687887444cafc502c15683f3972cf6308e6b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302828"
---
# <a name="system-functions"></a>系统函数
下表列出了 ODBC 标量函数集中包含的系统函数。 通过使用 SQL_SYSTEM_FUNCTIONS 的*信息类型*调用**SQLGetInfo** ，应用程序可以确定驱动程序支持哪些系统功能。  
  
 表示为*exp*的参数可以是列的名称、其他标量函数的结果或文本，其中，基础数据类型可以表示为 SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL、SQL_DOUBLE、SQL_TYPE_DATE、SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 表示为*值*的参数可以是文本常量，其中，基础数据类型可表示为 SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL、SQL_DOUBLE、SQL_TYPE_DATE、SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 返回的值表示为 ODBC 数据类型。  
  
|函数|说明|  
|--------------|-----------------|  
|**DATABASE （）** （ODBC 1.0）|返回与连接句柄相对应的数据库的名称。 （通过使用 SQL_CURRENT_QUALIFIER 连接选项调用**SQLGetConnectOption** ，也可以使用数据库的名称。）|  
|**IFNULL （** _exp_，_value_**）** （ODBC 1.0）|如果*exp*为 null，则返回*值*。 如果*exp*不为 null，则返回*exp* 。 可能的数据类型或*值*类型必须与*exp*数据类型兼容。|  
|**USER （）** （ODBC 1.0）|返回 DBMS 中的用户名。 （通过指定信息类型，还可以通过**SQLGetInfo**使用该用户名： SQL_USER_NAME。）此名称可以不同于登录名。|
