---
title: SQL Server Native Client 11.0 中的 UTF-16 支持 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b28d869a6e33969550751158e321ec24062bf6ac
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707150"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支持
  从开始 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ，如果在绑定列结果或输出参数时提供固定长度的缓冲区，并且如果在 `wchar` 终止字符之前写入缓冲区的字符是代理项对的高代理项码位，并且下一个 `wchar` 字符是低代理项代码点，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 将不会向缓冲区添加高代理项码位。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
