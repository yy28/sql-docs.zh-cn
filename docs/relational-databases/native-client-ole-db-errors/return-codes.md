---
title: 返回代码 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8c5d922c22cf067c0ef8ebb14ce8842df90370f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32944442"
---
# <a name="return-codes"></a>返回代码
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在最基本的级别上，成员函数要么成功，要么失败。 在稍微精确一些的级别上，函数可能会成功，但是它的成功可能并不是应用程序开发人员想要的成功。  
  
 有关 OLE DB 返回代码的详细信息，请参阅[返回代码 (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631)。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序成员函数将返回 S_OK，成功的函数。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序成员函数不返回，则为 S_OK，OLE/COM HRESULT 解压缩失败和 IS_ERROR 宏可以确定总体的成功或失败的函数。  
  
 如果失败或 IS_ERROR 返回 TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使用者将确定成员函数执行失败。 当失败或 IS_ERROR 返回 FALSE，HRESULT 不等于，则为 S_OK， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使用者将确定该函数成功在某种意义上。 使用者可以检索在此"成功信息与"从返回的详细的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序错误接口。 此外，函数清楚地失败 （失败宏返回 TRUE） 的情况，扩展的错误信息将从可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序错误接口。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序使用者通常会遇到与信息 DB_S_ERRORSOCCURRED"成功"HRESULT 返回。 通常，返回 DB_S_ERRORSOCCURRED 的成员函数会定义一个或多个将状态值传递给使用者的参数。 除了在状态值参数中返回的错误信息之外，使用者无法获得其他任何错误信息，因此使用者应将应用程序逻辑实现为在有可用的状态值时检索这些状态值。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序成员函数不返回成功代码 S_FALSE。 所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序成员函数始终返回以指示成功，则为 S_OK。  
  
## <a name="see-also"></a>另请参阅  
 [错误](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
