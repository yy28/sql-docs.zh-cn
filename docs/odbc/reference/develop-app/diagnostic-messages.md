---
title: "诊断消息 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic messages messages
- error messages [ODBC], diagnostic messages
- diagnostic messages [ODBC]
ms.assetid: 98027871-9901-476e-a722-ee58b7723c1f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a242628af9898a3a437ec11000de626135e9d79
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="diagnostic-messages"></a>诊断消息
诊断消息将返回每个 SQLSTATE 带。 使用大量不同的消息通常返回相同的 SQLSTATE。 例如，为 SQL 语法中的大多数错误返回 SQLSTATE 42000 （语法错误或访问冲突）。 但是，每个语法错误很可能可以通过不同的消息进行描述。  
  
 SQLSTATEs 附录 A 中和每个函数中的表中的错误列中列出示例诊断消息。 尽管驱动程序可以返回这些消息，但它们都更有可能返回的数据源的任何消息传递给它们。  
  
 应用程序通常显示给用户，以及 SQLSTATE 和本机错误代码的诊断消息。 这有助于用户和技术支持人员确定任何问题的原因。 消息中嵌入的组件信息是这种做法特别有用。  
  
 诊断消息来自于数据源和 ODBC 连接，如驱动程序、 网关和驱动程序管理器中的组件。 通常情况下，数据源不能直接支持 ODBC。 因此，如果 ODBC 连接中的组件从数据源收到一条消息，它必须标识为消息的源的数据源。 它必须还将自己标识为接收消息的组件。  
  
 如果错误或警告的源是一个组件本身，诊断消息必须说明这。 因此，消息的文本具有两个不同的格式。 对于错误和警告的操作不会发生数据源中，诊断消息必须使用此格式：  
  
 **[** *供应商标识符* **] [** *ODBC 组件标识符* **]** *组件提供文本*  
  
 对于错误和数据源中出现的警告，诊断消息必须使用此格式：  
  
 **[** *供应商标识符* **] [** *ODBC 组件标识符* **] [** *数据源标识符* **]** *数据源-提供的文本*  
  
 下表显示每个元素的含义。  
  
|元素|含义|  
|-------------|-------------|  
|*供应商标识符*|标识在其中发生错误或警告，或直接从数据源接收错误或警告的组件的供应商联系。|  
|*ODBC 组件标识符*|标识在其中发生错误或警告，或直接从数据源接收错误或警告的组件。|  
|*数据源标识符*|标识的数据源。 对于基于文件的驱动程序，这通常是一种文件格式，例如 Xbase [1] 基于为 DBMS 的驱动程序，这是 DBMS 产品。|  
|*组件提供文本*|ODBC 组件生成。|  
|*数据源-提供的文本*|生成的数据源。|  
  
 [1] 在此情况下，该驱动程序充当的驱动程序和数据源。  
  
 方括号 (**[]**) 必须包含在消息中，不能证明是可选项。
