---
title: 返回代码 | Microsoft Docs
description: 返回代码
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- OLE DB Driver for SQL Server, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
author: pmasl
ms.author: pelopes
ms.openlocfilehash: a1deedd8903f69268ebc5e7f5caafaa79a7f7b18
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994924"
---
# <a name="return-codes"></a>返回代码
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在最基本的级别上，成员函数要么成功，要么失败。 在稍微精确一些的级别上，函数可能会成功，但是它的成功可能并不是应用程序开发人员想要的成功。  
  
 有关 OLE DB 返回代码的详细信息，请参阅 [Return Codes (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631)（返回代码 (OLE DB)）。  
  
 如果 OLE DB Driver for SQL Server 的某成员函数返回 S_OK，则表明该函数执行成功。  
  
 如果适用于 SQL Server 的 OLE DB 驱动程序的成员函数未返回 S_OK，则 OLE/COM HRESULT-unpacking FAILED 和 IS_ERROR 宏判断此函数总体上是否成功。  
  
 如果 FAILED 或 IS_ERROR 返回 TRUE，则适用于 SQL Server 的 OLE DB 驱动程序的使用者可确定成员函数执行失败。 如果 FAILED 或 IS_ERROR 返回 FALSE，并且 HRESULT 不等于 S_OK，则 OLE DB Driver for SQL Server 的使用者可以肯定函数在某种意义上执行成功。 使用者可在适用于 SQL Server 的 OLE DB 驱动程序错误接口返回的“成功但存在错误”消息中检索详细信息。 此外，如果函数明显执行失败（FAILED 宏返回 TRUE），也可从适用于 SQL Server 的 OLE DB 驱动程序错误接口获取详细的错误信息。  
  
 OLE DB Driver for SQL Server 的使用者经常会遇到 HRESULT 返回 DB_S_ERRORSOCCURRED“成功但存在错误”。 通常，返回 DB_S_ERRORSOCCURRED 的成员函数会定义一个或多个将状态值传递给使用者的参数。 除了在状态值参数中返回的错误信息，使用者无法获得其他任何错误信息，因此使用者需将应用程序实现为存在状态值可检索这些值。  
  
 OLE DB Driver for SQL Server 成员函数不返回成功代码 S_FALSE。 OLE DB Driver for SQL Server 的所有成员函数总是返回 S_OK 来指示执行成功。  
  
## <a name="see-also"></a>另请参阅  
 [错误](../../oledb/ole-db-errors/errors.md)  
  
  
