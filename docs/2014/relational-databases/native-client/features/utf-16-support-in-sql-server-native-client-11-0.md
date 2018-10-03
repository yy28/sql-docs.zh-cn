---
title: SQL Server Native Client 11.0 中的 utf-16 支持 |Microsoft Docs
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
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48226717"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支持
  从开始[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，如果绑定列结果或输出参数时提供了一个固定长度缓冲区和如果`wchar`终止字符是代理项对的高代理项代码点之前，如果写入到缓冲区的字符下一步`wchar`字符是一个低代理项码位[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端将不向缓冲区添加高代理项码位。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
