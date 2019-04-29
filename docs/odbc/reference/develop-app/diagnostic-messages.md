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
manager: craigg
ms.openlocfilehash: 883cd29d8628f1e9270ae95a772c4d116b896710
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63034914"
---
# <a name="diagnostic-messages"></a>诊断消息
带有每个返回的诊断消息。 有很多不同的消息的通常返回相同的 SQLSTATE。 例如，SQL 语法中的大多数错误返回 SQLSTATE 42000 （语法错误或访问冲突）。 但是，每个语法错误很可能通过不同的消息进行描述。  
  
 示例诊断消息 SQLSTATEs 附录 A 中和每个函数中的表中的错误列中列出。 尽管驱动程序可以返回这些消息，它们是更有可能返回由数据源的任何消息传递给它们。  
  
 应用程序通常显示给用户，以及 SQLSTATE 和本机错误代码的诊断消息。 这有助于用户和支持人员确定任何问题的原因。 消息中嵌入的组件信息是这种做法特别有用。  
  
 诊断消息来自数据源和 ODBC 连接，如驱动程序、 网关和驱动程序管理器中的组件。 通常情况下，数据源不直接支持 ODBC。 因此，如果 ODBC 连接中的一个组件收到消息时从数据源，它必须作为消息源的标识数据源。 它必须还将自身标识为接收消息的组件。  
  
 如果出现错误或警告的源是一个组件本身，诊断消息必须说明这。 因此，消息的文本具有两个不同的格式。 错误和警告的数据源中不会发生，诊断消息必须使用以下格式：  
  
 **[** *vendor-identifier* **][** *ODBC-component-identifier* **]** *component-supplied-text*  
  
 对于错误和数据源中出现的警告，诊断消息必须使用以下格式：  
  
 **[** *vendor-identifier* **][** *ODBC-component-identifier* **][** *data-source-identifier* **]** *data-source-supplied-text*  
  
 下表显示了每个元素的含义。  
  
|元素|含义|  
|-------------|-------------|  
|*vendor-identifier*|标识在其中发生错误或警告，或直接从数据源收到的错误或警告的组件的供应商联系。|  
|*ODBC-component-identifier*|标识在其中发生错误或警告，或直接从数据源收到的错误或警告的组件。|  
|*data-source-identifier*|标识数据源。 对于基于文件的驱动程序，这通常是一种文件格式，例如 Xbase [1] 基于为 DBMS 的驱动程序，这是 DBMS 产品。|  
|*component-supplied-text*|ODBC 组件生成。|  
|*data-source-supplied-text*|生成的数据源。|  
  
 [1] 在这种情况下，该驱动程序充当驱动程序和数据源。  
  
 方括号 (**[]**) 必须包含在消息，并表明可选项。
