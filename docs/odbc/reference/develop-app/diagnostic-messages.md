---
title: 诊断消息 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic messages messages
- error messages [ODBC], diagnostic messages
- diagnostic messages [ODBC]
ms.assetid: 98027871-9901-476e-a722-ee58b7723c1f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 39ebda5de5820cdfd7333ad1d0997593922e0a4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039889"
---
# <a name="diagnostic-messages"></a>诊断消息
每个 SQLSTATE 返回一条诊断消息。 相同的 SQLSTATE 通常返回了大量不同的消息。 例如，对于 SQL 语法中的大多数错误，都将返回 SQLSTATE 42000 （语法错误或访问冲突）。 但是，每个语法错误都可能由不同的消息描述。  
  
 示例诊断消息列在 "附录 A" 中的 SQLSTATEs 表的 "错误" 列和每个函数中。 尽管驱动程序可以返回这些消息，但它们更有可能返回数据源传递给它们的任何消息。  
  
 应用程序通常向用户显示诊断消息，以及 SQLSTATE 和本机错误代码。 这可以帮助用户和支持人员确定任何问题的原因。 在执行此操作时，消息中嵌入的组件信息特别有用。  
  
 诊断消息来自 ODBC 连接（如驱动程序、网关和驱动程序管理器）中的数据源和组件。 通常，数据源不直接支持 ODBC。 因此，如果 ODBC 连接中的组件接收到来自数据源的消息，它必须将数据源标识为消息源。 它还必须将自身标识为收到消息的组件。  
  
 如果错误或警告的源是组件本身，则诊断消息必须说明这一点。 因此，消息文本具有两种不同的格式。 对于数据源中未出现的错误和警告，诊断消息必须使用以下格式：  
  
 **[** *供应商标识符* **] [** *ODBC 组件标识符* **]** *组件提供的文本*  
  
 对于数据源中发生的错误和警告，诊断消息必须使用以下格式：  
  
 **[** *供应商标识符* **] [** *ODBC 组件标识符* **] [** *数据源标识符* **]** *数据源提供的文本*  
  
 下表显示了每个元素的含义。  
  
|元素|含义|  
|-------------|-------------|  
|*供应商标识符*|标识发生错误或警告的组件的供应商，或直接从数据源接收错误或警告的组件的供应商。|  
|*ODBC 组件标识符*|标识出现错误或警告或直接从数据源接收错误或警告的组件。|  
|*数据源标识符*|标识数据源。 对于基于文件的驱动程序，这通常是一种文件格式，如用于基于 DBMS 的驱动程序的 Xbase [1]，这是 DBMS 产品。|  
|*组件提供的文本*|由 ODBC 组件生成。|  
|*数据源提供的文本*|由数据源生成。|  
  
 [1] 在本例中，驱动程序同时充当驱动程序和数据源。  
  
 括号（**[]**）必须包含在消息中，并且不表示可选项。
