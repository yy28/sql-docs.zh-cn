---
title: 多个活动的结果集 (MARS)
description: 介绍当 SqlDataReader 的每个实例从单独的命令启动时，如何在一个连接上打开多个 SqlDataReader。
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 7097dc3717966d441cd669ddccd189c2510211aa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452143"
---
# <a name="multiple-active-result-sets-mars"></a>多个活动的结果集 (MARS)

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

多个活动的结果集（MARS）是一项功能，允许在单个连接上执行多个批处理。 在以前的版本中，一次只能对单个连接执行一个批处理。 通过 MARS 执行多个批处理并不意味着同时执行操作。  
  
## <a name="in-this-section"></a>在本节中  
[启用多重活动结果集](enable-multiple-active-result-sets.md)  
讨论如何在 SQL Server 中使用 MARS。  
  
[操作数据](manipulate-data.md)  
提供对 MARS 应用程序进行编码的示例。  
  
## <a name="related-sections"></a>相关章节  
[异步操作](asynchronous-operations.md)  
提供有关在 .NET 中使用新的异步功能的详细信息。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
