---
title: 返回代码 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 625d56a38d88b3cccbea1c75ad88917af1a6f6dd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63228942"
---
# <a name="return-codes"></a>返回代码
  在最基本的级别上，成员函数要么成功，要么失败。 在稍微精确一些的级别上，函数可能会成功，但是它的成功可能并不是应用程序开发人员想要的成功。  
  
 有关 OLE DB 返回代码的详细信息，请参阅 [Return Codes (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631)（返回代码 (OLE DB)）。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序成员函数返回 S_OK 时，该函数将成功。  
  
 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序成员函数未返回 S_OK，则 OLE/COM HRESULT 解压缩失败，IS_ERROR 宏可以确定函数的总体成功或失败。  
  
 如果 FAILED 或 IS_ERROR 返回 TRUE，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可确保成员函数执行失败。 如果失败或 IS_ERROR 返回 FALSE，并且 HRESULT 不等于 S_OK，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使用者可确保函数在某种程度上成功。 使用者可以从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序错误接口返回有关此 "包含信息成功" 的详细信息。 此外，在函数明显失败的情况下（失败的宏返回 TRUE）， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序错误接口提供了扩展的错误信息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者通常会遇到 "信息成功" HRESULT 返回 DB_S_ERRORSOCCURRED。 通常，返回 DB_S_ERRORSOCCURRED 的成员函数会定义一个或多个将状态值传递给使用者的参数。 除了在状态值参数中返回的错误信息之外，使用者无法获得其他任何错误信息，因此使用者应将应用程序逻辑实现为在有可用的状态值时检索这些状态值。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序成员函数不会返回成功代码 S_FALSE。 所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序成员函数始终返回 S_OK 以指示成功。  
  
## <a name="see-also"></a>另请参阅  
 [错误](errors.md)  
  
  
