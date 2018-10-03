---
title: 创建数据源 （数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d7107c32-69ed-49a8-9b6e-32753eebf42c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01f576ceb6b465dd8238972d29456300a01837df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128167"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>创建数据源（数据挖掘基础教程）
  一个*数据源*是保存和管理在项目中并部署到的数据连接应用[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库。 除了其他所有必需的连接属性外，数据源还包含源数据所在的服务器和数据库的名称。  
  
> [!IMPORTANT]  
>  数据库的名称为 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]。 如果尚未安装此数据库，请参阅[Microsoft SQL 示例数据库](http://go.microsoft.com/fwlink/?LinkId=88417)页。  
  
### <a name="to-create-a-data-source"></a>创建数据源  
  
1.  在中**解决方案资源管理器**，右键单击**数据源**文件夹，然后选择**新数据源**。  
  
2.  上**欢迎使用数据源向导**页上，单击**下一步**。  
  
3.  上**选择如何定义连接**页上，单击**新建**添加到连接[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]数据库。  
  
4.  在中**提供程序**列表中**连接管理器**，选择**本机 OLE DB\SQL Server Native Client 11.0**。  
  
5.  在中**服务器名称**框中，键入或选择要安装的服务器的名称[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]。  
  
     例如，键入**localhost**如果本地服务器上承载该数据库。  
  
6.  在中**登录到服务器**组中，选择**使用 Windows 身份验证**。  
  
    > [!IMPORTANT]  
    >  实施者应尽可能使用 Windows 身份验证，因为它提供的身份验证方法比 SQL Server 身份验证更加安全。 而提供 SQL Server 身份验证只是为了向后兼容。 有关身份验证方法的详细信息，请参阅[数据库引擎配置-帐户预配](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md)。  
  
7.  在中**选择或输入数据库名称**列表中，选择[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]，然后单击**确定**。  
  
8.  单击“下一步” 。  
  
9. 上**模拟信息**页上，单击**使用服务帐户**，然后单击**下一步**。  
  
     上**完成向导**页上，请注意，默认情况下，数据源名为 Adventure Works DW 2012。  
  
10. 单击 **“完成”**。  
  
     新数据源 Adventure Works DW 2012 将显示**数据源**在解决方案资源管理器中的文件夹。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建数据源视图&#40;数据挖掘基础教程&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [创建 Analysis Services 项目&#40;数据挖掘基础教程&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [创建数据源（SSAS 多维）](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [定义数据源](../analysis-services/lesson-1-2-defining-a-data-source.md)   
 [设置模拟选项&#40;SSAS-多维&#41;](../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)  
  
  
