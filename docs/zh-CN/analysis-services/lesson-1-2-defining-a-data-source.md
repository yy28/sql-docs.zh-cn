---
title: 定义了一个数据源 |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5a3e83c9-8788-431e-85b0-a68c79377ff3
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: dfeaa3291327ab2ee848acf30db017a60c4b3258
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-2---defining-a-data-source"></a>课程 1-2-定义了一个数据源
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

在创建 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目后，通常通过定义项目使用的一个或多个数据源来开始使用项目。 定义数据源时，将定义要用于连接此数据源的连接字符串信息。 有关详细信息，请参阅 [创建数据源（SSAS 多维）](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)。  
  
在以下任务中，您将把 AdventureWorksDWSQLServer2012 示例数据库定义为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目的数据源。 为了实现本教程教学目的，此数据库位于您的本地计算机上，而源数据库通常驻留在一台或多台远程计算机中。  
  
### <a name="to-define-a-new-data-source"></a>定义新的数据源  
  
1.  在解决方案资源管理器中（在 Microsoft Visual Studio 窗口的右侧），右键单击“数据源”，然后单击“新建数据源”。  
  
2.  上**欢迎使用数据源向导**页**数据源向导**，单击**下一步**以打开**选择如何定义连接**页。  
  
3.  在“选择如何定义连接”页上，可以基于新连接、现有连接或以前定义的数据源对象来定义数据源。 在本教程中，基于新连接定义数据源。 确保已选中“基于现有连接或新连接创建数据源”，再单击“新建”。  
  
4.  在“连接管理器”对话框中，为数据源定义连接属性。 在“提供程序”列表框中，确保已选中“本机 OLE DB\SQL Server Native Client 11.0”。  
  
    [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 此外支持其他提供程序，它显示在**提供程序**列表。  
  
5.  在“服务器名称”文本框中，键入 **localhost**。  
  
    若要连接到本地计算机上的命名实例，键入**localhost\\<instance name>**。 若要连接到特定的计算机而不是本地计算机，请键入该计算机名称或 IP 地址。  
  
6.  确保已选中“使用 Windows 身份验证”。 在“选择或输入数据库名称”列表中，选择 **AdventureWorksDW2012**。  
  
7.  单击“测试连接”以测试与数据库的连接。  
  
8.  单击“确定”，然后单击“下一步”。  
  
9. 在该向导的“模拟信息”页上，可以定义 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用于连接数据源的安全凭据。 在选中“Windows 身份验证”时，模拟会影响用于连接数据源的 Windows 帐户。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不支持模拟来处理 OLAP 对象。 选择“使用服务帐户”，然后单击“下一步”。  
  
10. 在“完成向导”页上，接受默认名称 **Adventure Works DW 2012**，然后单击“完成”以创建新数据源。  
  
> [!NOTE]  
> 若要在创建数据源之后修改其属性，请在“数据源”文件夹中双击该数据源，以在“数据源设计器”中显示数据源属性。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[定义数据源视图](../analysis-services/lesson-1-3-defining-a-data-source-view.md)  
  
## <a name="see-also"></a>另请参阅  
[创建数据源（SSAS 多维）](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
