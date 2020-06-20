---
title: 包安装向导 UI 参考 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.deploymentwizard.confirminstallation.f1
- sql12.dts.deploymentwizard.deploydtspackages.f1
- sql12.dts.deploymentwizard.selectinstfolder.f1
- sql12.dts.deploymentwizard.specifytargetsqlserver.f1
- sql12.dts.deploymentwizard.welcome.f1
- sql12.dts.deploymentwizard.finish.f1
- sql12.dts.deploymentwizard.configurepackages.f1
- sql12.dts.deploymentwizard.packagevalidation.f1
helpviewer_keywords:
- Package Installer Wizard
ms.assetid: 6fca44d9-5001-4644-bcf3-c2d10a674b97
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b51049f0a55a10ae83af9e0f253c1c717f6d4962
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964853"
---
# <a name="package-installation-wizard-ui-reference"></a>包安装向导 UI 参考
  可以使用 **“包安装向导”** 部署 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目（包括包、所包含的杂项文件以及所有包的依赖关系）。  
  
 在部署包之前，可以先创建配置，然后再将其与包一起进行部署。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 在运行时使用配置来动态更新包和包对象的属性。 例如，通过提供将值映射到包含连接字符串的属性的配置，可在运行时动态设置 OLE DB 连接的连接字符串。  
  
 只有在生成 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目并创建部署实用工具后，方可运行包安装向导。 有关详细信息，请参阅 [Deploy Packages by Using the Deployment Utility](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)。  
  
 以下部分介绍了该向导中的各页。  
  
## <a name="welcome-to-the-package-installation-wizard-page"></a>“欢迎使用包安装向导”页  
 可以使用 **“包安装向导** ”部署为其生成包部署实用工具的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
 **不再显示此起始页**  
 选择此选项可以在下次运行向导时跳过起始页。  
  
 **下一步**  
 转到向导的下一页。  
  
 **完成**  
 跳到“完成包安装向导”页。 如果返回到向导前面的页修改所选项，并指定了所有必需的选项，则可以使用此选项。  
  
## <a name="configure-packages-page"></a>“配置包”页  
 可以使用 **“配置包”** 页编辑包配置。  
  
### <a name="options"></a>选项  
 **配置文件**  
 通过从列表中选择文件，可以编辑配置文件的内容。  
  
 **相关主题：** [创建包配置](../../2014/integration-services/create-package-configurations.md)  
  
 **路径**  
 查看要配置的属性的路径。  
  
 **类型**  
 查看属性的数据类型。  
  
 **值**  
 指定配置的值。  
  
 **下一步**  
 转到向导的下一页。  
  
 **完成**  
 跳到“完成包安装向导”页。 如果返回到向导前面的页修改所选项，并指定了所有必需的选项，则可以使用此选项。  
  
## <a name="confirm-installation-page"></a>“确认安装”页  
 可以使用 **“确认安装”** 页开始安装包，查看状态以及查看向导用于从指定项目中安装文件的信息。  
  
 **下一步**  
 安装包及其相关文件，并在完成安装后转到下一个向导页。  
  
 **状态**  
 显示包的安装进度。  
  
 **完成**  
 转到“完成包安装向导”页。 如果返回到向导前面的页修改所选项，并指定了所有必需的选项，则可以使用此选项。  
  
## <a name="deploy-ssis-packages-page"></a>“部署 SSIS 包”页  
 可以使用 **“部署 SSIS 包”** 页指定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包及其依赖关系的安装位置。  
  
### <a name="options"></a>选项  
 **部署到文件系统**  
 将包及其依赖关系部署到文件系统内指定的文件夹中。  
  
 **部署到 SQL Server**  
 将包及其依赖关系部署到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例中。 如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在服务器之间共享包，请使用此选项。 将所有包依赖关系安装在文件系统内指定的文件夹中。  
  
 **安装后验证包**  
 指示安装后是否验证包。  
  
 **下一步**  
 转到向导的下一页。  
  
 **完成**  
 跳到“完成包安装向导”页。 如果返回到向导前面的页修改所选项，并指定了所有必需的选项，则可以使用此选项。  
  
## <a name="packages-validation-page"></a>“包验证”页  
 可以使用 **“包验证”** 页查看包验证的进度和结果。  
  
 **下一步**  
 转到向导的下一页。  
  
## <a name="select-installation-folder-page"></a>“选择安装文件夹”页  
 可以使用 **“选择安装文件夹”** 页，指定在文件系统中安装包及其依赖关系的文件夹。  
  
### <a name="options"></a>选项  
 **文件夹**  
 指定包及其依赖关系要复制到的路径和文件夹。  
  
 **浏览**  
 使用“查找文件夹”**** 对话框找到目标文件夹。  
  
 **下一步**  
 转到向导的下一页。  
  
 **完成**  
 跳到“完成包安装向导”页。 如果已经复查完前面向导页中的选项，并指定了所有必需的选项，则可以使用此选项。  
  
## <a name="specify-target-sql-server-page"></a>“指定目标 SQL Server”页  
 可以使用 **“指定目标 SQL Server”** 页，指定将包部署到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的选项。  
  
### <a name="options"></a>选项  
 **服务器名称**  
 指定要部署包的服务器的名称。  
  
 **Use Windows Authentication**  
 指定是否使用 Windows 身份验证来登录到服务器。 为了实现更好的安全性，建议使用 Windows 身份验证。  
  
 **使用 SQL Server 身份验证**  
 指定包是否应使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证来登录到服务器。 如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，则必须提供用户名和密码。  
  
 **用户名**  
 指定用户名。  
  
 **密码**  
 指定密码。  
  
 **包路径**  
 指定逻辑文件夹的名称，或者输入 "/" 作为默认文件夹。  
  
 若要在 " **SSIS 包**" 对话框中选择该文件夹，请单击 "浏览（...）"。但是，该对话框不提供选择默认文件夹的方法。 如果要使用默认文件夹，则必须在该文本框中输入 "/"。  
  
> [!NOTE]  
>  如果您没有输入有效的包路径，则会出现下面的错误消息：“一个或多个参数无效”。  
  
 **依靠服务器存储进行加密**  
 选择此项可以使用 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的安全功能来帮助保护包。  
  
 **下一步**  
 转到向导的下一页。  
  
 **完成**  
 跳到“完成包安装向导”页。 如果返回到向导前面的页修改所选项，并指定了所有必需的选项，则可以使用此选项。  
  
## <a name="finish-the-package-installation-page"></a>“完成包安装”页  
 可以使用 **“完成包安装向导”** 页查看包安装结果的摘要。 此页提供了如所部署 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目的名称、已安装的包、配置文件和安装位置等之类的详细信息。  
  
 **完成**  
 单击“完成”**** 即可退出该向导。  
  
## <a name="see-also"></a>另请参阅  
 [包部署 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
