---
title: FOR XML 对用户定义数据类型 (UDT) 的支持 | Microsoft Docs
description: 了解在使用 FOR XML 子句时对用户定义数据类型 (UDT) 的支持。
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 53a70da583b55fa8d979aeaaee3782fd6551c6ea
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729919"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>用户定义数据类型 (UDT) 的 FOR XML 支持
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  FOR XML 不支持公共语言运行时 (CLR) 用户定义数据类型 (UDT)。  
  
 若要将 FOR XML 与 CLR 用户定义数据类型结合使用，请确保该数据类型具有 XML 序列化，并在 FOR XML select 子句中使用到 XML 的显式转换。  
  
## <a name="see-also"></a>另请参阅  
 [各种 SQL Server 数据类型的 FOR XML 支持](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
