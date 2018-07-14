---
title: 创建目标的邮件挖掘模型结构 （数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a9c67f29-0c47-4a5a-862b-db0f5213c2c9
caps.latest.revision: 54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c9c760ddd7f5445dfc00cc7c40ef877269940383
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282233"
---
# <a name="creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial"></a>创建目标邮件挖掘模型结构（数据挖掘基础教程）
  要创建目标邮件方案，第一步是使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的数据挖掘向导创建新的挖掘结构和决策树挖掘模型。  
  
 在此任务将设置新的挖掘结构，并添加初始挖掘模型基于[!INCLUDE[msCoName](../includes/msconame-md.md)]决策树算法。 若要创建此结构，需要首先选择表和视图，然后标识将用于定型的列和将用于测试的列。  
  
### <a name="to-create-a-mining-structure-for-the-targeted-mailing-scenario"></a>创建用于目标邮件方案的挖掘结构  
  
1.  在解决方案资源管理器中右键单击**挖掘结构**，然后选择**新建挖掘结构**以启动数据挖掘向导。  
  
2.  在 **“欢迎使用数据挖掘向导”** 页上，单击 **“下一步”**。  
  
3.  上**选择定义方法**页上，确认**从现有关系数据库或数据仓库**已选择，然后单击**下一步**。  
  
4.  上**创建数据挖掘结构**页面上，在**想要使用何种数据挖掘技术？**，选择**Microsoft 决策树**。  
  
    > [!NOTE]  
    >  如果收到警告，告知无法找到数据挖掘算法，则项目属性可能配置不正确。 当项目尝试从 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器检索数据挖掘算法列表却找不到服务器时，就会出现此警告。 默认情况下[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]将使用**localhost**与服务器。 如果要使用其他实例或命名实例，则必须更改项目属性。 有关详细信息，请参阅[创建 Analysis Services 项目&#40;数据挖掘基础教程&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)。  
  
5.  单击“下一步” 。  
  
6.  上**选择数据源视图**页上，在**可用数据源视图**窗格中，选择**Targeted Mailing**。 可以单击**浏览**若要查看数据源视图中的表，然后单击**关闭**以返回到向导。  
  
7.  单击“下一步” 。  
  
8.  上**指定表类型**页上，选择中的复选框**用例**vTargetMail 以将其用作事例表，然后单击的列**下一步**。 稍后您将使用 ProspectiveBuyer 表进行测试，不过现在可以忽略它。  
  
9. 上**指定定型数据**页上，将标识至少一个可预测列、 一个键列，以及一个输入为您的模型的列。 选择中的复选框**可预测**中的列**BikeBuyer**行。  
  
    > [!NOTE]  
    >  请注意窗口底部的警告。 你将不能选择至少一个之前，导航到下一页**输入**和一个**可预测**列。  
  
10. 单击**建议**以打开**提供相关列建议**对话框。  
  
     **建议**按钮处于启用状态，只要已选中至少一个可预测属性。 **提供相关列建议**对话框列出了最紧密相关的可预测列的列，并通过使用可预测属性及其关联顺序属性。 显著相关的列（置信度高于 95%）将被自动选中以添加到模型中。  
  
     查看建议，然后依次**取消**toignore 建议。  
  
    > [!NOTE]  
    >  如果单击**确定**，所有列出的建议会被标记为在向导中的输入列。 如果仅同意其中的某些建议，则必须手动更改值。  
  
11. 验证中的复选框**键**中选择列**CustomerKey**行。  
  
    > [!NOTE]  
    >  如果数据源视图中的源表表示一个键，则数据挖掘向导将自动选择该列作为模型的键。  
  
12. 选择中的复选框**输入**下列行中的列。 可通过下面的方法来同时选中多个列：突出显示一系列单元格，然后在按住 Ctrl 的同时选中一个复选框。  
  
    -   **年龄**  
  
    -   **CommuteDistance**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **性别**  
  
    -   **GeographyKey**  
  
    -   **HouseOwnerFlag**  
  
    -   **MaritalStatus**  
  
    -   **NumberCarsOwned**  
  
    -   **NumberChildrenAtHome**  
  
    -   **地区**  
  
    -   **TotalChildren**  
  
    -   **YearlyIncome**  
  
13. 在该页的最左侧的列中，选中以下行中的复选框。  
  
    -   **AddressLine1**  
  
    -   **AddressLine2**  
  
    -   **DateFirstPurchase**  
  
    -   **EmailAddress**  
  
    -   **FirstName**  
  
    -   **姓氏**  
  
     确保这些行仅选择了左侧列中的复选标记。 这些列将添加到结构中，但不会包含在模型中。 但是，模型生成后，它们将可用于钻取和测试。 有关钻取详细信息，请参阅[钻取查询&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
14. 单击“下一步” 。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [指定数据类型和内容类型&#40;数据挖掘基础教程&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [指定表类型&#40;数据挖掘向导&#41;](../../2014/analysis-services/specify-table-types-data-mining-wizard.md)   
 [数据挖掘设计器](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 决策树算法](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)  
  
  
