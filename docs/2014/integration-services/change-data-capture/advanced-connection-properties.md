---
title: 高级连接属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4edfab68-7e68-45e8-a3f3-a0049ff7eb9e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a7a5744aa2adcaab74ca09bbb962c8c69d985b79
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771513"
---
# <a name="advanced-connection-properties"></a>高级连接属性
  使用 **“高级连接属性”** 对话框可以将更多连接参数添加到连接字符串。  
  
 其他连接参数可以是您正在使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库实例支持的任何 ODBC 连接参数。  
  
 使用 **“高级连接属性”** 对话框添加的参数将添加到在 **“连接到 SQL Server”** 对话框中选择的参数上。  
  
 所提供的各个参数的最后一个实例均覆盖该参数的任何以前的实例。 使用 **“高级连接参数”** 添加的参数将跟踪并替换 **“SQL Server 连接”** 对话框中提供的参数。 例如，如果“SQL Server 连接”  对话框将服务器名称指定为 SERVER1，而“其他连接参数”  页包含 ;SERVER=SERVER2，则会连接到 SERVER2。  
  
 使用 **“高级连接属性”** 对话框添加的参数将作为纯文本传递。  
  
> [!IMPORTANT]  
>  不要在 **“高级连接属性”** 对话框中包含登录凭据。 否则，它们将在没有加密的情况下通过网络传递。  
  
## <a name="see-also"></a>另请参阅  
 [访问 CDC 设计器控制台](access-the-cdc-designer-console.md)   
 [用于实例创建的 SQL Server 连接](sql-server-connection-for-instance-creation.md)  
  
  
