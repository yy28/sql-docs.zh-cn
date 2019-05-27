---
title: 使用部署实用工具部署包 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], installing
- installing packages
- dependencies [Integration Services]
- deploying packages [Integration Services], installing
ms.assetid: eaf4b56e-2023-4d17-971c-703031da758c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 73b71e83f3b0f0f895b2cc5b8fd3495fb4893a32
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059615"
---
# <a name="deploy-packages-by-using-the-deployment-utility"></a>使用部署实用工具部署包
  如果要使用所生成的部署实用工具将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中的包安装到与生成该工具的计算机不同的其他计算机上，则必须首先将部署文件夹复制到目标计算机上。  
  
 部署文件夹的路径是在为其创建部署实用工具的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目的 DeploymentOutputPath 属性中指定的。 默认路径为 bin\Deployment，它相对于 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象。 有关详细信息，请参阅 [Create a Deployment Utility](../../2014/integration-services/create-a-deployment-utility.md)。  
  
 可以使用包安装向导安装包。 若要启动向导，在将部署文件夹复制到服务器之后，请双击部署实用工具文件。 此文件名为 \<项目名称>.SSISDeploymentManifest，可以在目标计算机上的部署文件夹找到它。  
  
> [!NOTE]  
>  如果并行安装了不同版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，根据你部署的包的版本，可能会遇到错误。 因为 .SSISDeploymentManifest 文件扩展名对于 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的所有版本是相同的，因此可能出现此错误。 针对最近安装的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]版本双击该文件调用安装程序 (dtsinstall.exe)，它的版本可能与部署实用工具文件的版本不同。 若要解决这个问题，请从命令行运行正确的 dtsinstall.exe 版本，并且提供部署实用工具文件的路径。  
  
 包安装向导指导您完成将包安装到文件系统或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的步骤。 可以按下列方式配置安装：  
  
-   选择安装包的位置类型和位置。  
  
-   选择安装包的依赖项的位置。  
  
-   在目标服务器上安装包之后对其进行验证。  
  
 包的基于文件的依赖项始终都安装到文件系统中。 如果要将包安装到文件系统中，则依赖项也会安装到您为包所指定的文件夹中。 如果将包安装到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，您可以指定存储基于文件的依赖项的文件夹。  
  
 如果包包括要进行修改以便在目标计算机上使用的配置，您可以使用该向导更新属性的值。  
  
 除了使用包安装向导安装包之外，还可以使用 **dtutil** 命令提示实用工具来复制和移动包。 有关详细信息，请参阅 [dtutil Utility](dtutil-utility.md)。  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>将包部署到 SQL Server 的实例  
  
1.  在目标计算机上打开部署文件夹。  
  
2.  双击清单文件（\<项目名称>.SSISDeploymentManifest），以启动包安装向导。  
  
3.  在 **“部署 SSIS 包”** 页上，选择 **“SQL Server 部署”** 选项。  
  
4.  还可以选择 **“安装后验证包”** ，以便在将包安装到目标服务器之后对其进行验证。  
  
5.  在 **“指定目标 SQL Server”** 页上，指定要将包安装到的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，并选择身份验证模式。 如果选择 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，则必须提供用户名和密码。  
  
6.  在 **“选择安装文件夹”** 页上，指定文件系统中用来安装包依赖项的文件夹。  
  
7.  如果包包括配置，可以通过更新“配置包”页上 **“值”** 列表中的值来编辑这些配置。  
  
8.  如果选择了在安装之后验证包，请查看所部署的包的验证结果。  
  
## <a name="see-also"></a>请参阅  
 [打包部署&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
