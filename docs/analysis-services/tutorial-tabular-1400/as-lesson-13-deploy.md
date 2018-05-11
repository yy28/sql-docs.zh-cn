---
title: Analysis Services 教程课 13： 部署 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57ddfe2f2d00b098fbffa40811a7877752fefed4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="deploy"></a>部署

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，你配置部署属性：指定要将部署到的服务器和模型的名称。 然后将模型部署到服务器。 您的模型部署后，用户可以通过使用报表的客户端应用程序连接到它。 若要了解详细信息，请参阅[部署到 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)和[表格模型解决方案部署](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)。  
  
学完本课的估计时间： **5 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文摘自表格建模教程中，应按顺序完成。 之前在本课程中执行任务，你应完成上一课：[课 12： 在 Excel 中分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)。  

> [!IMPORTANT]  
> 如果将部署到 Azure Analysis Services，你必须具有[管理员权限](https://docs.microsoft.com/azure/analysis-services/analysis-services-server-admins)serever 上。  

> [!IMPORTANT]  
> 如果你已 AdventureWorksDW 示例数据库安装在本地 SQL 服务器上，并且正在将您的模型部署到 Azure Analysis Services 服务器，[本地数据网关](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway)是必需的。
  
## <a name="deploy-the-model"></a>部署模型  
  
#### <a name="to-configure-deployment-properties"></a>配置部署属性  

  
1.  在**解决方案资源管理器**，右键单击**AW Internet Sales**项目，，然后单击**属性**。  
  
2.  在**AW Internet 销售属性页**对话框中，在**部署服务器**中**服务器**属性，输入完整的服务器名称。 如果连接到 Azure Analysis Services，服务器名称必须包括完整的 URL。

    ![作为-lesson13-部署-属性](../tutorial-tabular-1400/media/as-lesson13-deploy-property.png)
  
3.  在**数据库**属性中，键入**Adventure Works Internet Sales**。  
  
4.  在**模型名称**属性中，键入**Adventure Works Internet 销售模型**。  
  
5.  验证所做的选择，然后单击“确定”。  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>若要部署 Adventure Works Internet Sales
  
1.  在**解决方案资源管理器**，右键单击**AW Internet Sales**项目 >**生成**。  

2.  右键单击**AW Internet Sales**项目 >**部署**。

    将部署到 Azure Analysis Services，系统可能提示你输入你的帐户。 输入你的组织帐户和密码，例如nancy@adventureworks.com。此帐户必须是管理员在服务器上。
  
    部署对话框中出现，并显示元数据和模型中包含每个表的部署状态。  
    
    ![as-lesson13-deploy-status](../tutorial-tabular-1400/media/as-lesson13-deploy-status.png)
  
3. 成功完成部署后，继续操作并单击“关闭”。  
  

本课程介绍要部署 SSDT 中的表格模型的最常见且最简单方法。 如部署向导或使用 XMLA 和 AMO 使自动化的高级的部署选项提供更大的灵活性、 一致性以及计划的部署。 若要了解详细信息，请参阅[表格模型解决方案部署](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)。

## <a name="conclusion"></a>结语  
恭喜！ 完创作和部署你的第一个 Analysis Services 表格模型。 本教程已帮助指导您完成了创建表格模型的最常见任务。 既然已部署了 Adventure Works Internet Sales Model，就可以使用 SQL Server Management Studio 来管理此模型、创建进程脚本和备份计划。 用户现在还可以连接到模型时使用的报表的客户端应用程序，例如 Microsoft Excel 或 Power BI。  

![作为 lesson13 ssms](../tutorial-tabular-1400/media/as-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>下一步是什么？
[使用 Power BI Desktop 连接](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect-pbi)   
[补充课程-动态安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)   
[补充课程-详细信息行](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)   
[补充课程-不规则层次结构](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)   
