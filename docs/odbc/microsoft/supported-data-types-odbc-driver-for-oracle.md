---
title: 支持的数据类型（Oracle ODBC 驱动程序） |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 313254a3a117984d666d7c7be7e506386ae34e3b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301112"
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>支持的数据类型（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 用于 Oracle 的 ODBC 驱动程序支持所有 Oracle 7.3 数据类型;但是，它不支持此处列出的任何新的 Oracle8 数据类型。  
  
|数据类型|Oracle 7。3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|不适用|不支持|  
|BLOB|不适用|不支持|  
|CHAR|支持|支持|  
|CLOB|不适用|不支持|  
|DATE|支持|支持|  
|FLOAT|支持|支持|  
|INTEGER|支持|支持|  
|LONG|支持|支持|  
|LONG RAW|支持|支持|  
|NCHAR|不适用|不支持|  
|NCLOB|不适用|不支持|  
|NUMBER|支持|支持|  
|NVARCHAR2|不适用|不支持|  
|RAW|支持|支持|  
|VARCHAR2|支持|支持|  
|MLSLABEL|不支持。|不支持。|  
  
> [!NOTE]  
>  有关 VARCHAR 列允许大小的详细信息，请参阅本指南中的[Varchar 列大小](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md)。
