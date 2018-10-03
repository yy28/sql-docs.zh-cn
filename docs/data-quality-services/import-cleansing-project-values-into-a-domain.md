---
title: 将清理项目值导入到域中 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.importprojectvalues.f1
ms.assetid: f23e38e2-39e0-42d7-abd5-34d8fcca5d2a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a79a860b30a94c5514c91922354a9a82c30e4148
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647715"
---
# <a name="import-cleansing-project-values-into-a-domain"></a>将清理项目值导入到域中

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中，您可以将在清理过程中从数据质量清理项目或包含 DQS 清理组件的集成服务包中收集的数据质量知识，导入到域中。 这样可确保可信知识不丢失，而且可以不断地改进知识库。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   若要将清理项目值导入到域中，该域必须已在 Data Quality Client 的清理项目中或包含 DQS 清理组件的集成服务包中使用。  
  
-   Data Quality Client 中的清理项目或包含 DQS 清理组件的集成服务包必须已成功完成。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须具有 DQS_MAIN 数据库的 dqs_kb_editor 或 dqs_administrator 角色，才能将在清理过程中收集的数据质量知识导入到域中。  
  
##  <a name="Import"></a> 导入清理项目值  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，在域管理活动中打开知识库。  
  
3.  如果将值添加到某个现有域中，则在域列表中选择该域。  
  
4.  单击 **“域值”** 选项卡，在图标栏中单击 **“导入值”** 图标，然后单击 **“导入项目值”**。 此时将显示 **“导入项目值”** 对话框，其中包含使用该域进行清理的数据质量项目以及集成服务包的列表。  
  
    > [!NOTE]  
    >  如果尚未使用域或其任何链接域创建项目，或者项目没有完成，则 **“导入项目值”** 选项将不可用。  
  
5.  在 **“导入项目值”** 对话框中：  
  
    -   在 **“已导入”** 下拉列表中选择 **“全部”** 以显示所有项目，或选择 **“否”** 仅显示尚未导入值的项目。  
  
    -   选择要从中导入值的项目。  
  
    -   如果选择 **“从‘新建’选项卡中添加值”** ，则除了 **“正确”** 和 **“已更正”** 选项卡中的值之外，还将导入新建选项卡中的值。  
  
    -   单击“确定” 。  
  
6.  您将返回到 **“域值”** 选项卡；在值成功导入后，将显示一条消息。 **“值”** 表中将显示已导入的值，因此也是首次进入域中的值。  
  
7.  取消选择 **“仅显示新内容”** 以显示域中的所有值。  
  
8.  选择 **“正确”**、 **“错误”** 或 **“无效”** 以仅显示具有所选类型的值。  
  
9. 若要搜索特定字符串，在 **“查找”** 文本框中输入该字符串。 单击向上或向下箭头可以逐一查看满足搜索条件的值。 这些值将突出显示为黄色。  
  
10. 单击 **“完成”**。  
  
    > [!NOTE]  
    >  有关使用 **“域值”** 选项卡上的值的详细信息，请参阅 [Change Domain Values](../data-quality-services/change-domain-values.md)。  
  
##  <a name="FollowUp"></a> 跟进：将项目值导入到域后  
 将在清理过程中收集的数据质量知识导入到域中后，您可以对该域和值执行其他域管理任务。 有关详细信息，请参阅[管理域](../data-quality-services/managing-a-domain.md)。  
  
##  <a name="Values"></a> 要导入的值  
 下面的值将从项目导入到域中：  
  
-   仅字符串值导入到域中。  
  
-   将只导入 **“清理”** 活动的 **“管理和查看结果”** 页上 **“正确”** 、 **“已更正”** 和 **“新建”** 选项卡上的值。 如果在 **“导入项目值”** 对话框中选中了 **“从‘新建’选项卡中添加值”** 复选框，将只导入 **“新建”** 选项卡中的值。  
  
-   值将作为正确的值或具有更正的错误值进行导入。 仅导入具有更正值的错误值。  
  
-   更正值将为知识库中不存在的新值或现有的正确值。  
  
-   仅将在值级别上（而不是记录级别）执行的更正导入到知识库中。  
  
-   如果导入的值与域规则相矛盾，则会创建无效值。  
  
-   如果您一次导入多个项目中的值，这些值按先后顺序导入。  
  
-   域中因基于字词的关系而导致的更正值将作为正确值（不是错误）导入。  
  
##  <a name="ValuesNot"></a> 不会导入的值  
 下面的值将不会从项目导入到域中：  
  
-   不会导入 **“清理”** 活动的 **“管理和查看结果”** 页上 **“建议”** 和 **“无效”** 选项卡上的值。  
  
-   如果在清理项目中找到的值与域中的现有值冲突，则跳过在该项目中找到的值。 这将包括清理值与知识库值之间的冲突。  
  
-   不会将在记录级别执行的更正导入到知识库中。  
  
-   如果要替换的值已被引用数据服务更正或批准为正确的，则不会将该值导入到域中。  
  
-   如果某个更正值在知识库中显示为无效或错误的值，则无论是错误值还是更正值都不会被导入。  
  
-   如果域作为复合域的一部分且对复合域执行清理，将不会导入任何值。  
  
-   仅当知识库处于工作状态且知识库由正在执行导入的用户锁定，才可从项目中导入值。  
  
## <a name="see-also"></a>另请参阅  
 [数据清理](../data-quality-services/data-cleansing.md)   
 [DQS 清理转换](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
