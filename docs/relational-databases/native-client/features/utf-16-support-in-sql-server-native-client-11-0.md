---
title: SQL Server Native Client 11.0 中的 utf-16 支持 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cdb3291ddb036ecaad803884145a6bd87b455cf9
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43092529"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  从开始[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，如果绑定列结果或输出参数时提供了一个固定长度缓冲区，并且**wchar**字符写入到缓冲区之前终止字符是一个高代理项代码点代理项对，并且如果下一步**wchar**字符是一个低代理项码位[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端将不向缓冲区添加高代理项码位。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
