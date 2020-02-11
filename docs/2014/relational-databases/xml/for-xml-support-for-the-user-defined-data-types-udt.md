---
title: 用户定义数据类型 (UDT) 的 FOR XML 支持 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e41f5a97c4b32611589e5da24a95e237416a5b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63204993"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>用户定义数据类型 (UDT) 的 FOR XML 支持
  FOR XML 不支持公共语言运行时 (CLR) 用户定义数据类型 (UDT)。  
  
 若要将 FOR XML 与 CLR 用户定义数据类型结合使用，请确保该数据类型具有 XML 序列化，并在 FOR XML select 子句中使用到 XML 的显式转换。  
  
## <a name="see-also"></a>另请参阅  
 [各种 SQL Server 数据类型的 FOR XML 支持](for-xml-support-for-various-sql-server-data-types.md)  
  
  
