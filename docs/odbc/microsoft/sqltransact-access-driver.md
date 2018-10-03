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
manager: craigg
ms.openlocfilehash: b0cb17ed043a6b533b007769b9cbb28652d06e6f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47719603"
---
# <a name="sqltransact-access-driver"></a>SQLTransact（Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 使用 Microsoft Access 驱动程序时，为支持 SQL_COMMIT 和 SQL_ROLLBACK *fType*调用中的参数**SQLTransact**。  
  
 如果在提交过程中发生故障，可以使用修复数据库选项在 Microsoft Access 驱动程序设置中，或通过使用中的 REPAIR_DB 关键字修复受影响的数据库**SQLConfigDataSource**函数。
