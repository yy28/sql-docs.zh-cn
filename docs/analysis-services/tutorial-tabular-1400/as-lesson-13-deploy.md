---
title: Analysis Services 教程第 13 课：部署 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: ab561b096c4436349580201eec3b3ea10a8aaa75
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685304"
---
# <a name="deploy"></a>部署

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课中，配置部署属性;指定要将部署到的服务器和模型的名称。 然后将模型部署到服务器。 部署您的模型后，用户可以通过使用报表客户端应用程序连接到它。 若要了解详细信息，请参阅[部署到 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)并[表格模型解决方案部署](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)。  
  
学完本课的预计时间：**5 分钟**  
  
## <a name="prerequisites"></a>先决条件  

本文是表格建模教程应按顺序完成的一部分。 执行任务之前在本课程中，您应当已完成上一课：[第 12 课：在 Excel 中分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)。  

> [!IMPORTANT]  
> 如果部署到 Azure Analysis Services，您必须具有[管理员权限](https://docs.microsoft.com/azure/analysis-services/analysis-services-server-admins)serever 上。  

> [!IMPORTANT]  
> 如果在本地 SQL Server 上，安装了 AdventureWorksDW 示例数据库，并且要将模型部署到 Azure Analysis Services 服务器，[的本地数据网关](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway)是必需的。
  
## <a name="deploy-the-model"></a>部署模型  
  
#### <a name="to-configure-deployment-properties"></a>配置部署属性  

  
1.  在中**解决方案资源管理器**，右键单击**AW Internet Sales**项目，并单击**属性**。  
  
2.  在中**AW Internet Sales 属性页**对话框中的**部署服务器**，在**Server**属性，输入完整的服务器名称。 如果连接到 Azure Analysis Services，服务器名称必须包括完整的 URL。

    ![as-lesson13-deploy-property](../tutorial-tabular-1400/media/as-lesson13-deploy-property.png)
  
3.  在中**数据库**属性中，键入**Adventure Works Internet Sales**。  
  
4.  在中**模型名称**属性中，键入**Adventure Works Internet Sales Model**。  
  
5.  验证所做的选择，然后单击“确定”。  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>若要部署 Adventure Works Internet Sales
  
1.  在中**解决方案资源管理器**，右键单击**AW Internet Sales**项目 >**生成**。  

2.  右键单击**AW Internet Sales**项目 >**部署**。

    部署到 Azure Analysis Services 时，你可能会提示输入你的帐户。 输入你的组织帐户和密码，例如nancy@adventureworks.com。 此帐户必须是管理员组中，在服务器上。
  
    部署对话框中将出现并显示的元数据和模型中包含每个表的部署状态。  
    
    ![as-lesson13-deploy-status](../tutorial-tabular-1400/media/as-lesson13-deploy-status.png)
  
3. 成功完成部署后，继续操作并单击“关闭”。  
  

本课程介绍如何部署从 SSDT 表格模型的最常见且最简单方法。 例如，部署向导或使用 XMLA 和 AMO 自动执行的高级的部署选项提供更大的灵活性、 一致性和计划部署的部署。 若要了解详细信息，请参阅[表格模型解决方案部署](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)。

## <a name="conclusion"></a>结束语  
祝贺你！ 您完成创作和部署第一个 Analysis Services 表格模型。 本教程已帮助指导您完成了创建表格模型的最常见任务。 既然已部署了 Adventure Works Internet Sales Model，就可以使用 SQL Server Management Studio 来管理此模型、创建进程脚本和备份计划。 用户现在还可以连接到在模型中使用的报告的客户端应用程序，例如 Microsoft Excel 或 Power BI。  

![as-lesson13-ssms](../tutorial-tabular-1400/media/as-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>下一步是什么？
[使用 Power BI Desktop 连接](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect-pbi)   
[补充课程-动态安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)   
[补充课程-详细信息行](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)   
[补充课程-不规则层次结构](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)   
