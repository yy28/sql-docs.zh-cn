---
title: SQLTransact （Access 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4d4b3d8d417591bd72dde22240c81a91d80f990
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948975"
---
# <a name="sqltransact-access-driver"></a>SQLTransact（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 使用 Microsoft Access 驱动程序时，对**SQLTransact**的调用中的*fType*参数支持 SQL_COMMIT 和 SQL_ROLLBACK。  
  
 如果在提交过程中发生故障，则可以使用 Microsoft Access 驱动程序安装程序中的 "修复数据库" 选项，或在**SQLConfigDataSource**函数中使用 REPAIR_DB 关键字来修复受影响的数据库。
