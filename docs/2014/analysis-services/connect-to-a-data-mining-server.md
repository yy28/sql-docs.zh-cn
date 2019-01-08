---
title: 连接到数据挖掘服务器 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
- getting started
ms.assetid: 85962ad6-d840-4bc6-905e-c667c3276944
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9ca50a030fef65c9de02bc93dcd970df2686b0a
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52420388"
---
# <a name="connect-to-a-data-mining-server"></a>连接到数据挖掘服务器
  ![连接按钮](media/misc-connection.gif "连接按钮")  
  
 单击**连接**按钮以选择现有连接，或创建新的连接到的实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
 **为什么需要连接到服务器？**  
  
 创建连接后，将允许您使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器提供的数据挖掘算法，以及利用服务器的优化处理。  
  
 不必将数据或结果保存到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库或 SQL Server 数据库中。 Excel 数据挖掘外接程序只能使用在 Excel 中存储的数据，或者使用作为 Excel 数据源连接到的数据。  
  
## <a name="how-to-create-a-new-connection"></a>如何创建新连接  
  
1.  单击**连接**按钮。  
  
2.  在中**Analysis Services 连接**对话框中，单击**新建**。  
  
3.  在中**连接到 Analysis Services**对话框框中，键入服务器名称。  
  
4.  指定身份验证方法。  
  
5.  指定将在其中存储数据挖掘模型的目录或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。  
  
    > [!NOTE]  
    >  如果尚未创建任何数据库，则您可以使用“(默认值)”来创建连接，然后测试连接；然而，无法向默认连接添加挖掘模型。 创建任何挖掘模型之前，应该创建到现有数据库的连接。  
  
6.  如果是通过 Web 服务连接到服务器，请键入该 Web 服务所需的用户名和密码。  
  
7.  键入新连接的友好名称。  
  
8.  单击**测试连接**以验证该服务器是否可用。  
  
## <a name="troubleshooting-connections"></a>排除连接故障  
 本节回答了有关与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的连接的一些常见问题。  
  
 **我收到消息，指出"未找到任何连接。"**  
  
 如果显示该按钮的下半部分中的文本**无连接**，这意味着你尚未创建连接到[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库，或连接失败。 您可以继续处理来自 Access 或其他数据源的 Excel 中的数据，但如果要创建数据挖掘模型或运行预测查询，则必须拥有活动连接。  
  
 **假设我没有使用服务器的权限？**  
  
 如果您不具有足够的权限在服务器上存储挖掘模型或如果你想要试验数据挖掘而无需保存所做的工作，可以使用表分析工具创建临时数据结构和临时模型。 您仍需要能在服务器上存储临时模型。 让管理员允许使用*会话挖掘模型*在服务器上。  
  
 如果您想确保保存模型，可以禁用使用临时模型的选项，或可以在数据挖掘客户端中使用向导。 这些向导在服务器上存储所有模型。 您将需要对存储模型的数据库具有管理访问权限，所以，我们建议您让管理员创建一个数据库，该数据库专门用于使用外接程序创建挖掘模型。  
  
 **我的连接; 断开未丢失我的所有工作？**  
  
 如果终止与服务器的连接，您的结果和数据将不会丢失，因为它们存储在 Excel 中。 但是，如果您创建了一些临时模型，则在一个较短的时间后这些模型将从服务器中删除。 因此如果暂时失去连接，一段时间模型不会被删除。  
  
 生成的任何数据或结果将不丢失，因为所有报表和表存储在 Excel 中。  
  
> [!NOTE]  
>  外接程序与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器进行通信时，不要断开与服务器或网络的连接。 例如，不要在创建模型或处理数据时断开连接。 在某些情况下，可能会损坏您的数据。  
  
 **我无法连接到在模型中使用 Visio 工具**  
  
 Visio 数据挖掘模板无法使用临时挖掘结构和模型。 若要创建某个挖掘模型的关系图，该模型必须存储在服务器上。  
  
 **如何监视连接的使用情况？**  
  
 [Trace &#40;Excel 数据挖掘客户端&#41;](trace-data-mining-client-for-excel.md)工具创建的外接程序和指定的服务器之间的所有活动的日志。  
  
 若要启用会话模型的监视，请选择**使用会话模型**选项**跟踪**对话框。  
  
 通过跟踪，您可以在创建模型和结构时查看生成的 DMX 和 XMLA 命令。 您还可以查看客户端为在 Excel 中生成结果和报告而发送的查询。  
  
 **什么是临时模型？如何保存临时模型？**  
  
 默认情况下，Excel 表分析工具创建临时数据结构和挖掘模型。 只要保持工作簿打开并且不从 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 断开连接，即可持续浏览和查询临时模型。  
  
 只要您关闭 Excel 工作簿，或者更改或结束与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的连接，则创建的所有结构和模型都将被删除。  
  
 在您在 Excel 数据挖掘客户端中完成某一向导后，模型将默认保存到服务器中，但在每个向导的最后一页上，存在用来使用临时模型的选项。 如果选择此选项，则所创建的数据挖掘结构和模型都将存储在一个临时文件中。 只要 Excel 保持打开状态，您就可浏览、管理和修改结构和模型。 但是，关闭 Excel 后，该结构及其相关模型都将被删除。  
  
 您可以显式创建临时结构或模型使用**数据挖掘高级查询编辑器**并选择 DMX 模板之一。 添加 `USE SESSION MODELS` 子句可指定对象是临时的。   
  
### <a name="creating-backups-of-mining-models-and-structures"></a>创建挖掘模型和结构的备份  
 若要创建模型或结构的备份，可以导出使用它[管理模型&#40;SQL Server 数据挖掘外接程序&#41;](manage-models-sql-server-data-mining-add-ins.md)，在 Excel 数据挖掘客户端。  
  
 如果您创建了一个临时挖掘模型，该模型通常具有难于理解的名称，例如 Table5_593679_TS_62446。 但是，可以使用[Trace &#40;Excel 数据挖掘客户端&#41;](trace-data-mining-client-for-excel.md)工具，用于发现临时结构和模型创建的表分析工具的名称，然后备份它们使用**管理模型**。  
  
##### <a name="identify-and-export-a-temporary-model"></a>标识和导出临时模型  
  
1.  在中**连接**组的数据挖掘客户端 Excel，请单击**跟踪**。  
  
2.  查看连接活动日志，并且通过查看列和可预测输出定位模型（举例）。  
  
     高级的用户：如果您熟悉 DMX 或 XMLA，您可以将语句复制到文件以备今后使用。  
  
3.  在您找到临时模型和结构的名称，打开**管理模型**和选择的模型。  
  
4.  单击“导出此挖掘模型”以便在您指定的位置中生成一个脚本文件。  
  
## <a name="see-also"></a>请参阅  
 [连接到源数据&#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)   
 [服务器配置实用程序&#40;Excel 数据挖掘外接程序&#41;](server-configuration-utility-data-mining-add-ins-for-excel.md)  
  
  
