---
title: 支持的数据类型 （Oracle ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: 21d5f8d9-a3aa-4aa4-bc37-ff8bc90c0870
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 145170afee5ab791602695c662ce1e80e86cae7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915673"
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>支持的数据类型（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 Oracle ODBC 驱动程序支持所有 Oracle 7.3 数据类型;但是，它不支持任何此处列出的新 Oracle8 数据类型。  
  
|数据类型|Oracle 7.3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|不适用|不支持|  
|BLOB|不适用|不支持|  
|CHAR|支持|支持|  
|CLOB|不适用|不支持|  
|DATE|支持|支持|  
|FLOAT|支持|支持|  
|整数|支持|支持|  
|LONG|支持|支持|  
|LONG RAW|支持|支持|  
|NCHAR|不适用|不支持|  
|NCLOB|不适用|不支持|  
|NUMBER|支持|支持|  
|NVARCHAR2|不适用|不支持|  
|RAW|支持|支持|  
|VARCHAR2|支持|支持|  
|MLSLABEL|不提供支持。|不提供支持。|  
  
> [!NOTE]  
>  VARCHAR 列的允许大小的详细信息，请参阅[VARCHAR 列大小](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md)本指南中。
