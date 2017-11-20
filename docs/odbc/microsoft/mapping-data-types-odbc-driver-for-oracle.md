---
title: "映射数据类型 （适用于 Oracle 的 ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b6384f81f03a20e46a1d2a6434063caf32577554
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>数据类型映射 （适用于 Oracle 的 ODBC 驱动程序）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 在 Oracle 服务器支持一的组数据类型。 用于 Oracle 的 ODBC 驱动程序将这些数据类型映射到其相应的 ODBC SQL 数据类型。 下表列出 Oracle 7.3 Server 数据类型和其相应的 ODBC SQL 数据类型。  
  
 用于 Oracle 的 ODBC 驱动程序支持 Oracle 7.3 和某些 Oracle8 数据类型。 有关受支持 Oracle8 数据类型的详细信息，请参阅[支持的数据类型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)。  
  
|Oracle 服务器数据类型|ODBC SQL 数据类型|  
|-----------------------------|------------------------|  
|CHAR|SQL_CHAR|  
|DATE|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|整数|SQL_DECIMAL|  
|LONG|SQL_LONGVARCHAR|  
|LONG RAW|SQL_LONGVARBINARY|  
|NUMBER|SQL_DECIMAL|  
|RAW|SQL_VARBINARY|  
|VARCHAR2|SQL_VARCHAR|  
  
> [!NOTE]  
>  VARCHAR 列的允许大小的详细信息，请参阅[VARCHAR 列大小](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md)本指南中。

