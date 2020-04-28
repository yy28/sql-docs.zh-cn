---
title: 映射数据类型（Oracle ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 432c21b70efcdd63ef36bfe3d26f8488ddb11d1d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302668"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>映射数据类型（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 Oracle 服务器支持一组数据类型。 用于 Oracle 的 ODBC 驱动程序将这些数据类型映射到相应的 ODBC SQL 数据类型。 下表列出了 Oracle 7.3 服务器数据类型及其相应的 ODBC SQL 数据类型。  
  
 用于 Oracle 的 ODBC 驱动程序支持 Oracle 7.3 和某些 Oracle8 数据类型。 有关支持的 Oracle8 数据类型的详细信息，请参阅[支持的数据类型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)。  
  
|Oracle 服务器数据类型|ODBC SQL 数据类型|  
|-----------------------------|------------------------|  
|CHAR|SQL_CHAR|  
|DATE|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_DECIMAL|  
|LONG|SQL_LONGVARCHAR|  
|LONG RAW|SQL_LONGVARBINARY|  
|NUMBER|SQL_DECIMAL|  
|RAW|SQL_VARBINARY|  
|VARCHAR2|SQL_VARCHAR|  
  
> [!NOTE]  
>  有关 VARCHAR 列允许大小的详细信息，请参阅本指南中的[Varchar 列大小](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md)。
