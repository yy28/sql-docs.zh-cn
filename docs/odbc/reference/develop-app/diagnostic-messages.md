---
title: 诊断消息 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be63e9d78960e40ac5e9ee016d2cfd868d99a922
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305828"
---
# <a name="diagnostic-messages"></a>诊断消息
每个 SQLSTATE 都会返回一条诊断消息。 相同的 SQLSTATE 通常返回与许多不同的消息。 例如，SQLSTATE 42000（语法错误或访问冲突）返回，用于 SQL 语法中的大多数错误。 但是，每个语法错误可能由不同的消息描述。  
  
 示例诊断消息列在附录 A 和每个函数中的 SQLStatEs 表中的"错误"列中。 尽管驱动程序可以返回这些消息，但它们更有可能返回数据源传递给它们的任何消息。  
  
 应用程序通常向用户显示诊断消息以及 SQLSTATE 和本机错误代码。 这有助于用户和支持人员确定任何问题的原因。 消息中嵌入的组件信息在执行此操作时特别有用。  
  
 诊断消息来自 ODBC 连接中的数据源和组件，如驱动程序、网关和驱动程序管理器。 通常，数据源不直接支持 ODBC。 因此，如果 ODBC 连接中的组件从数据源接收消息，则必须将数据源标识为消息的来源。 它还必须将自己标识为接收消息的组件。  
  
 如果错误或警告的来源是组件本身，诊断消息必须解释这一点。 因此，消息的文本有两种不同的格式。 对于数据源中未发生的错误和警告，诊断消息必须使用此格式：  
  
 **[** *供应商标识符***] +** *ODBC-组件标识符* **=** *组件提供文本*  
  
 对于数据源中发生的错误和警告，诊断消息必须使用此格式：  
  
 **[** *供应商标识符* **] [** *ODBC-组件标识符***] 数据源***标识符* **=** *数据源提供文本*  
  
 下表显示了每个元素的含义。  
  
|元素|含义|  
|-------------|-------------|  
|*供应商标识符*|标识发生错误或警告或直接从数据源接收错误或警告的组件的供应商。|  
|*ODBC 组件标识符*|标识发生错误或警告或直接从数据源接收错误或警告的组件。|  
|*数据源标识符*|标识数据源。 对于基于文件的驱动程序，这通常是文件格式，例如 Xbase{1} 对于基于 DBMS 的驱动程序，这是 DBMS 产品。|  
|*组件提供文本*|由 ODBC 组件生成。|  
|*数据源提供文本*|由数据源生成。|  
  
 [1] 在这种情况下，驱动程序同时充当驱动程序和数据源。  
  
 括号 （*** ）** 必须包含在消息中，并且不指示可选项。
