---
title: UTF-16 支持
description: 从 SQL Server 2012 开始，了解 SQL Server Native Client 中固定长度缓冲区中的 UTF-16 支持。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3035a97394a552f11aec234ce856f1a85fecb46a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84948695"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  从开始 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ，如果在绑定列结果或输出参数时提供固定长度的缓冲区，并且如果在终止字符之前写入缓冲区中的**wchar**字符是代理项对的高代理项码位，并且下一个**wchar**字符是低代理项码位，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 将不会向缓冲区添加高代理项码位。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
