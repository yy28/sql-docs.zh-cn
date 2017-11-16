---
title: "用户定义数据类型 (UDT) 的 FOR XML 支持 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bbadd2f8f8b932e3d42c15230fe107d2489de524
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>用户定义数据类型 (UDT) 的 FOR XML 支持
  FOR XML 不支持公共语言运行时 (CLR) 用户定义数据类型 (UDT)。  
  
 若要将 FOR XML 与 CLR 用户定义数据类型结合使用，请确保该数据类型具有 XML 序列化，并在 FOR XML select 子句中使用到 XML 的显式转换。  
  
## <a name="see-also"></a>另请参阅  
 [各种 SQL Server 数据类型的 FOR XML 支持](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
