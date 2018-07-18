---
title: 系统函数 |Microsoft 文档
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
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5bfd40b587956595bfc8c35b4bb030543253cd9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913492"
---
# <a name="system-functions"></a>系统函数
下表列出了 ODBC 标量函数集中包括的系统函数。 通过调用**SQLGetInfo**与*信息类型*的 SQL_SYSTEM_FUNCTIONS，应用程序可以确定由驱动程序支持的系统函数。  
  
 自变量表示为*exp*可以是名称列中，另一个标量函数，或者是文本，其中基础数据类型无法表示为 SQL_NUMERIC、 SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL、 SQL_DOUBLE、 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 自变量表示为*值*可以是常量，其中基础数据类型可以表示为 SQL_NUMERIC、 SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL、 SQL_DOUBLE、 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 返回值表示为 ODBC 数据类型。  
  
|函数|Description|  
|--------------|-----------------|  
|**数据库 （)** (ODBC 1.0)|返回与连接句柄对应的数据库的名称。 (数据库的名称，也可以通过调用**SQLGetConnectOption**包含 SQL_CURRENT_QUALIFIER 连接选项。)|  
|**IFNULL (** *exp*，*值 * * *)** (ODBC 1.0)|如果*exp*为 null，*值*返回。 如果*exp*不为 null， *exp*返回。 可能的数据类型或类型的*值*必须与的数据类型兼容*exp*。|  
|**用户 （)** (ODBC 1.0)|在 DBMS 中返回的用户名。 (用户名称也是可**SQLGetInfo**通过指定信息类型： SQL_USER_NAME。)这可以是不同的登录名。|
