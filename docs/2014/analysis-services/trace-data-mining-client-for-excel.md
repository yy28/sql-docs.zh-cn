---
title: 跟踪 （数据挖掘客户端 for Excel） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tracer
- connections
ms.assetid: 4aea3e17-cd0f-48dd-8f22-b54a6c716426
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a62e3116fc9ba6bf3423faaf92b5374514174e42
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025258"
---
# <a name="trace-data-mining-client-for-excel"></a>跟踪（Excel 数据挖掘客户端）
  ![跟踪按钮](media/misc-trace.gif "跟踪按钮")  
  
 **跟踪**对话框可以帮助你监视发送到的实例的语句[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]你将用于数据挖掘。 创建连接到的实例后[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，客户端和服务器之间的所有交互都登录**跟踪**窗格中，包括创建结构、 添加挖掘模型，并使的语句预测，以及从服务器返回某些消息。  
  
 根据所请求的操作，该语句可能是数据挖掘扩展插件 (DMX) 数据定义查询或数据操作查询、Analysis Services 脚本语言 (ASSL) 包或者是对 Analysis Services 储存过程的调用。 但不会显示实际的数值结果和数据值。  
  
 **跟踪**监视仅当前的连接和的内容**跟踪**对话框中未存储。  
  
## <a name="options"></a>“常规”  
 “跟踪器”窗格  
 列出从 Excel 客户端发送到服务器的所有语句。  
  
 根据所请求的操作，该语句可能是 DMX 数据操作或数据定义语句、对 Analysis Services 储存过程的调用或者是 XML/A 数据包。  
  
 **当前连接**  
 单击此项可显示当前连接的定义。 该定义包括连接的名称、访问接口、数据源、目录、事务最近使用该连接的时间以及当前状态（“打开”、“不活动”等）。  
  
 **使用会话模型**  
 选中此复选框，则会在服务器中将数据挖掘模型和结构存储为临时对象。 您创建的模型和结构仅在当前会话期间可用。  
  
 取消选择此选项会通过将模型或结构存储到 Analysis Services 服务器中进行保存。  
  
 **请注意**仅当你使用 for Excel 表分析工具时，才，能够使用临时对象才可用。 Visio 数据挖掘模板和 Excel 数据挖掘客户端要求将结构和模型存储到服务器中。  
  
## <a name="tracing-temporary-structures-and-models"></a>跟踪临时结构和模型  
 如果使用的是表分析工具（默认情况下，该工具创建临时结构和模型），则服务器和客户端之间的活动将受到监视，但不会将您创建的模型或结构永久保存到服务器中。  
  
 如果你想要保留所做的工作，当使用一个表分析工具时，您可以取消选中选项，**使用会话模型**，若要使你的模型以永久保存在服务器上。 此外可以在复制中的语句**跟踪**到文件的窗格中，以便以后可以重新创建你的工作。  
  
## <a name="understanding-sessions"></a>了解会话  
 连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例时，数据挖掘外接程序将启动一个会话。 每个会话都会收到一个会话标识符，它用于标识 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例上的现有会话。 但会话标识符并不保证会话保持有效。 如果会话超时或与会话相关联的连接断开，则该会话将过期。 如果会话过期且不再有效，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将结束该会话，回滚正在处理的所有事务。 如果使用不再有效的会话标识符发送消息，则相应消息将失败，并显示一条错误指示无法找到指定的会话。  
  
 虽然某些数据挖掘模型显式存储在服务器上，但会话挖掘模型和结构不会显式存储在服务器上，并且会话数据挖掘活动的记录不会保留下来。 因为只要结束会话便会删除临时挖掘模型和结构，所以必须在保存任何要保留的工作之后再关闭 Excel 工作簿。  
  
## <a name="changing-connections"></a>更改连接  
 更改连接不会删除对先前连接的跟踪。 只有关闭工作簿才会清除会话。  
  
 如果在 Excel 工作簿中工作时更改连接，连接的更改不会记录在**跟踪**窗格。 若要显式显示的名称和当前连接的状态，必须单击**当前连接**。  
  
## <a name="understanding-statements-in-the-tracer"></a>了解跟踪器中的语句  
 DMX 是一种可用于在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中创建和使用数据挖掘模型的语言。 您可以使用 DMX 创建新数据挖掘模型的结构，为这些模型定型，并对其进行浏览、管理和预测。 DMX 由数据定义语言 (DDL) 语句、数据操作语言 (DML) 语句以及函数和运算符组成。  
  
 全面介绍 DMX 语句及其语法超出了本主题的讨论范围。 但是，你可以使用中的信息**跟踪**窗格中查找的行为的 DMX 语句的详细的信息。 Excel 数据挖掘外接程序还可帮助您生成复杂的 DMX 语句，并与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器进行交互。 有关详细信息，请参阅[查询&#40;SQL Server 数据挖掘外接程序&#41;](query-sql-server-data-mining-add-ins.md)。  
  
> [!NOTE]  
>  许多 DMX 语句都已参数化。 对于简单类型，参数的值在语句下列出。 但对于复杂类型，则仅列出参数的类型。  
  
 SQL Server Analysis Services 还使用 XML for Analysis (XMLA) 协议处理客户端应用程序（包括 Excel 数据挖掘客户端和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例）之间的所有通信。  
  
 有关 DMX 语法以及 XMLA 中的命令和元素的详细信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书。  
  
 发送到服务器的某些语句可能包含调用 Analysis Services 系统存储过程的查询。 有关详细信息，请参阅 SQL Server 联机丛书。  
  
  