---
title: 返回代码 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- SQL Server Native Client OLE DB provider, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
ms.assetid: 7f7457e9-fce4-400c-82e5-ee02e9e811c6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09056c9d4964ad10b2b25f63ef5991a1a7742cab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301012"
---
# <a name="return-codes"></a>返回代码
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在最基本的级别上，成员函数要么成功，要么失败。 在稍微精确一些的级别上，函数可能会成功，但是它的成功可能并不是应用程序开发人员想要的成功。  
  
 有关 OLE DB 返回代码的详细信息，请参阅 [Return Codes (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631)（返回代码 (OLE DB)）。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序成员函数返回S_OK时，该函数成功。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序成员函数不返回S_OK时，OLE/COM HRESULT 解包失败和IS_ERROR宏可以确定函数的总体成功或失败。  
  
 如果"失败"或"IS_ERROR返回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]TRUE，则本机客户端 OLE DB 提供程序使用者将确保成员函数执行失败。 当 FAILED 或 IS_ERROR返回 FALSE 且 HRESULT[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不等于S_OK时，本机客户端 OLE DB 提供程序使用者可以确信该函数在某种程度上成功。 使用者可以从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序错误接口检索有关此"成功信息"返回的详细信息。 此外，在函数明显失败的情况下（FAILED 宏返回 TRUE），从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序错误接口中提供了扩展的错误信息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序使用者通常遇到DB_S_ERRORSOCCURRED"成功与信息"HRESULT 返回。 通常，返回 DB_S_ERRORSOCCURRED 的成员函数会定义一个或多个将状态值传递给使用者的参数。 除了在状态值参数中返回的错误信息之外，使用者无法获得其他任何错误信息，因此使用者应将应用程序逻辑实现为在有可用的状态值时检索这些状态值。  
  
 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE DB 提供程序成员函数不返回成功代码S_FALSE。 所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序成员函数始终返回S_OK以指示成功。  
  
## <a name="see-also"></a>另请参阅  
 [错误](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
