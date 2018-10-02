---
title: 用户定义数据类型 (UDT) 的 FOR XML 支持 | Microsoft Docs
ms.custom: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8804977fd39dda2ec1d69830db677dd08daa4d25
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47602545"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>用户定义数据类型 (UDT) 的 FOR XML 支持
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  FOR XML 不支持公共语言运行时 (CLR) 用户定义数据类型 (UDT)。  
  
 若要将 FOR XML 与 CLR 用户定义数据类型结合使用，请确保该数据类型具有 XML 序列化，并在 FOR XML select 子句中使用到 XML 的显式转换。  
  
## <a name="see-also"></a>另请参阅  
 [各种 SQL Server 数据类型的 FOR XML 支持](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
