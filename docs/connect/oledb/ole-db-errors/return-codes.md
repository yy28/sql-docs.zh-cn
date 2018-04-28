---
title: 返回代码 |Microsoft 文档
description: 返回代码
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c9be88ab39a577a4751d119a76d74ed7ccc696e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="return-codes"></a>返回代码
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在最基本的级别上，成员函数要么成功，要么失败。 在稍微精确一些的级别上，函数可能会成功，但是它的成功可能并不是应用程序开发人员想要的成功。  
  
 有关 OLE DB 返回代码的详细信息，请参阅[返回代码 (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631)。  
  
 当 OLE DB Driver for SQL Server 成员函数返回时，则为 S_OK 时，则该函数成功。  
  
 当 SQL Server 成员函数用于 OLE DB 驱动程序不返回，则为 S_OK 时，OLE/COM HRESULT 解压缩失败和 IS_ERROR 宏可以确定总体成功或失败的函数。  
  
 如果失败或 IS_ERROR 返回 TRUE，OLE DB 驱动程序的 SQL Server 使用者将确定成员函数执行失败。 失败或 IS_ERROR 返回时 FALSE 和 HRESULT 不相等，则为 S_OK，使用者就可以确定该函数成功在某种意义上的 SQL Server 的 OLE DB 驱动程序。 使用者可以检索此"成功信息与"返回时从 SQL Server 错误接口的 OLE DB 驱动程序的详细的信息。 此外，在其中函数清楚地失败 （失败宏返回 TRUE） 的情况下，扩展的错误信息是 SQL Server 错误接口的 OLE DB 驱动程序中可用。  
  
 OLE DB 驱动程序的 SQL Server 使用者通常会遇到与信息 DB_S_ERRORSOCCURRED"成功"HRESULT 返回。 通常，返回 DB_S_ERRORSOCCURRED 的成员函数会定义一个或多个将状态值传递给使用者的参数。 没有错误消息可向使用者以外，返回在 status 值参数中，以便使用者应实现应用程序逻辑，以当它们可用时检索状态值。  
  
 因为 SQL Server 成员函数是 OLE DB 驱动程序不返回成功代码 S_FALSE。 所有 OLE DB 驱动程序对于 SQL Server 成员函数始终返回以指示成功，则为 S_OK。  
  
## <a name="see-also"></a>另请参阅  
 [错误](../../oledb/ole-db-errors/errors.md)  
  
  
