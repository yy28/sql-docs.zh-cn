---
title: "Integration Services 部署向导 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.deploymentwizard.f1"
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Integration Services 部署向导
  **Integration Services 部署向导**支持两种部署模型：
   - 项目部署模型
   - 包部署模型 
   
 **项目部署模型**允许将 SQL Server Integration Services (SSIS) 项目作为一个单元部署到 SSIS 目录中。
 
 **包部署模型**允许将已更新的包部署到 SSIS 目录中，而无需部署整个项目。 
 
 > **注意：**向导默认部署是项目部署模型。  
  
## 启动向导
通过以下方式之一启动向导：

 - 在 Windows Search 中键入**“SQL Server 部署向导”** 

**或**

 - 在 SQL Server 安装文件夹下搜索可执行文件 **ISDeploymentWizard.exe**；例如：“C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn”。 
 
 > **注意：**如果显示“简介”页，则单击“下一步”切换到“选择源”页。 
 
 对于每个部署模型，此页上的设置会有所不同。 基于你在此页中选择的模型，按照 [Project Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#ProjectModel) 部分或 [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) 部分的步骤进行操作。  
  
##  <a name="ProjectModel"></a> 项目部署模型  
  
### 选择源  
 若要部署你所创建的项目部署文件，请选择“项目部署文件”  并输入 .ispac 文件的路径。 若要部署位于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的项目，请选择 **“Integration Services 目录”**，然后输入目录中指向该项目的服务器名称和路径。 单击“下一步”  以查看“选择目标”  页。  
  
### 选择目标  
 若要在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中选择项目的目标文件夹，请输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例或单击 **“浏览”** 从服务器列表中选择。 然后输入 SSISDB 中的项目路径或单击 **“浏览”** 以选择此路径。 单击“下一步”  以查看“检查”  页。  
  
### 查看（和部署）  
 该页使你能够查看你所选择的设置。 可以通过单击 **“上一步”**或单击左窗格中的任意步骤来更改所做的选择。 单击“部署”  以启动部署过程。  
  
### 结果  
 部署过程完成之后，将看到“结果”  页。 该页显示每个操作是成功了还是失败了。 如果操作失败，单击 **“结果”** 列中的 **“失败”** 可以显示错误说明。 单击“保存报表...”  将结果保存到 XML 文件，或单击“关闭”  退出向导。  
  
##  <a name="PackageModel"></a> 包部署模型  
  
### 选择源  
 在“部署模型”  中选择“包部署”  选项后，“Integration Services 部署向导”  中的“选择源” 页会显示包部署模型的特定设置。  
  
 若要选择源包，请单击“浏览...” 按钮以选择包含包的“文件夹”，或在“包文件夹路径”文本框中键入文件夹路径，然后单击页面底部的“刷新”按钮。 现在，将可以在列表框中看见特定文件夹中的所有包。 默认情况下，所有的包都会被选中。 单击第一列中的“复选框”  以选择要部署到服务器的包。  
  
 请参阅“状态”  和“消息”  列以验证包的状态。 如果将状态设置为“就绪”  或“警告” ，部署向导则不会妨碍部署过程。 而如果将状态设置为“错误” ，向导则无法进一步部署所选包。 若要查看详细的警告/错误消息，请单击“消息”列中的链接。  
  
 如果使用密码加密敏感数据或包数据，请在“密码”  列中键入密码，然后单击“刷新”  按钮以验证是否接受此密码。 如果密码正确无误，状态将会更改为“就绪”  ，而且警告消息将会消失。 如果多个包都使用相同的密码，请选择具有相同加密密码的包，接着在“密码”  文本框中键入密码，然后单击“应用”  按钮。 该密码将应用到所选包。  
  
 如果所有选定包的状态未设置为“错误” ，则可使用“下一步”  按钮以继续进行包部署过程。  
  
### 选择目标  
 在选择包源后，单击“下一步”  按钮以切换到“选择目标”  页。 必须将包部署到 SSIS 目录 (SSISDB) 中的项目。 因此，在部署包之前，请确保 SSIS 目录中已存在该目标项目。 否则创建一个空项目。在“选择目标”页中，在“服务器名称”文本框中键入服务器名称，或单击“浏览…” 按钮以选择服务器实例。 然后单击“浏览…” 按钮以指定目标项目，此按钮位于“路径”文本框旁。 如果项目不存在，请单击“新建项目...” 以创建空项目作为目标项目。 **必须** 在文件夹下创建项目。  
  
### 查看和部署  
 在“选择目标”  页上单击“下一步”  以切换到“Integration Services 部署向导”  中的“审阅” 页。 在审阅页中，审阅有关部署操作的摘要报表。 验证之后，单击“部署”  按钮以执行部署操作。  
  
### 结果  
 部署完成之后，将看到“结果”  页。 在“结果”  页中，查看部署过程中每个步骤的结果。 在“结果”  页上，单击“保存报表”  以保存部署报表，或单击“关闭”  以关闭该向导。  
  
## 另请参阅  
 [将项目部署到 Integration Services 服务器](../../integration-services/packages/deploy-projects-to-integration-services-server.md)   
 [项目和包的部署](https://msdn.microsoft.com/library/hh213290.aspx)  
  
  