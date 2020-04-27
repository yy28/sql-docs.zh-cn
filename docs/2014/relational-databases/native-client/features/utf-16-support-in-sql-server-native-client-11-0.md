---
title: SQL Server Native Client 11.0 中的 UTF-16 支持 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 415cb2fe8a3295770cfc8bd2d5c6e56750adb6d9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63205121"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支持
  从开始[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，如果在绑定列结果或输出参数时提供固定长度的缓冲区，并且如果在终止`wchar`字符之前写入缓冲区的字符是代理项对的高代理项码位，并且下一个`wchar`字符是低代理项代码点， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]则 Native Client 将不会向缓冲区添加高代理项码位。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
