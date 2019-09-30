---
title: 步骤 4：部署第 6 课包 | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2a16cd38eef12584f8d876e610bfda5d602c3076
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283017"
---
# <a name="lesson-6-4-deploy-the-lesson-6-package"></a>第 6-4 课：部署第 6 课包

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



部署包涉及将包添加到 SQL Server 实例上 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中的 SSISDB 目录。 在本课程中，将第 6 课包添加到 SSISDB 目录，设置新参数，然后执行该包。 对于本课程，使用 SQL Server Management Studio 将第 6 课包添加到 SSISDB 目录，然后部署该包。 部署该包之后，修改参数以指向新位置，然后运行该包。   
在此任务中，将执行以下操作：  

1. 将包添加到 SQL Server 的 SSIS 节点中的 SSISDB 目录。  
  
2. 部署包。  
  
3. 设置包参数值。  

4. 在 SSMS 中执行包。  
  
## <a name="locate-or-add-the-ssisdb-catalog"></a>找到或添加 SSISDB 目录  
  
1.  依次选择“启动” > “所有程序” > “Microsoft SQL Server 2017”，然后选择“SQL Management Studio”     。  
  
2.  在“连接到服务器”对话框中，查看默认设置，然后选择“连接”   。 若要连接，“服务器”名称必须是安装 SQL Server 的计算机的名称  。 如果“数据库引擎”为命名实例，则“服务器”名称必须是格式为 \<计算机名>\\\<实例名> 的实例名称    。 
  
3.  在“对象资源管理器”中，展开“Integration Services 目录”   。  
  
4.  如果“Integration Services 目录”下未列出任何目录，请添加 SSISDB 目录  。  
  
5.  若要添加 SSISDB 目录，请右键单击“Integration Services 目录”，然后选择“创建目录”   。  
  
6.  在“创建目录”对话框上，选择“启用 CLR 集成”   。  
  
7.  在“密码”框中输入密码，然后在“重新键入密码”框中再次输入密码   。 
  
8.  选择“确定”，添加 SSISDB 目录  。  
  
## <a name="add-the-package-to-the-ssisdb-catalog"></a>将包添加到 SSISDB 目录  
  
1.  在“对象资源管理器”中，右键单击“SSISDB”，然后选择“创建文件夹”    。  
  
2.  在“创建文件夹”对话框中的“文件夹名称”框中输入 SSIS Tutorial，然后选择“确定”   。  
  
3.  展开“SSIS Tutorial”文件夹，右键单击“项目”，然后选择“导入包”    。  
  
4.  在“Integration Services 项目转换向导”的“简介”页上，选择“下一步”    。  
  
5.  在“查找包”页上，确保在“源”列表中选择“文件系统”，然后选择“浏览”     。  
  
6.  在“浏览文件夹”对话框中，浏览到包含此 SSIS Tutorial 项目的文件夹，然后选择“确定”   。  
  
7.  选择“下一步”  。  
  
8.  在“选择包”页上，应看到 SSIS Tutorial 中的所有六个包。 在“包”列表中，选择 Lesson 6.dtsx，然后选择“下一步”    。  
  
9. 在“选择目标”页上的“项目名称”框中输入 SSIS Tutorial Deployment，然后选择“下一步”     。

10. 在其余每个向导页上选择“下一步”，直到进入“检查”页面   。  
  
11. 在“检查”页上，选择“转换”   。  
  
12. 转换完成时，选择“关闭”  。  
  
关闭 Integration Services 项目转换向导时，SSIS 会显示 Integration Services 部署向导。 现在使用此向导部署第 6 课包。  
  
1.  在“Integration Services 部署向导”的“简介”页上，检查用于部署项目的步骤，然后选择“下一步”    。  
  
2.  在“选择目标”页上，验证服务器名称是否为包含 SSISDB 目录的 SQL Server 实例，以及路径是否显示 SSIS Tutorial Deployment，然后选择“下一步”    。  
  
3.  在“检查”页上检查“摘要”，然后选择“部署”    。  
  
4.  部署完成时，选择“关闭”  。  
  
5.  在“对象资源管理器”中，右键单击“Integration Services 目录”，然后选择“刷新”    。  
  
6.  展开“Integration Services 目录”，然后展开“SSISDB”   。 继续展开 SSIS Tutorial 下的树，直到完全展开项目  。 应在 SSIS Tutorial Deployment 节点的 Packages 节点下看到 Lesson 6.dtsx    。  
  
7.  若要验证该包是否完整，请右键单击 Lesson 6.dtsx，然后选择“配置”   。 在“配置”对话框中，选择“参数”，验证是否有一个条目将 Lesson 6.dtsx 作为“容器”、将 VarFolderName 作为“名称”并将 New Sample Data 的路径作为“值”，然后选择“关闭”         。  
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>创建并填充新的示例数据文件夹  
  
1.  在“Windows 资源管理器”中，在驱动器的根位置（例如，C:\\）创建名为 Sample Data Two 的新文件夹    。  
  
2.  打开[第 1 课先决条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)中的 Sample Data 文件夹，然后任意复制三个示例文件  。  
  
3.  浏览到 Sample Data Two 文件夹，然后粘贴已复制的文件  。  
  
## <a name="change-the-package-parameter-to-point-to-the-new-sample-data"></a>更改包参数以指向新示例数据  
  
1.  在“对象资源管理器”中，右键单击 Lesson 6.dtsx，然后选择“配置”    。  
  
2.  在“配置”对话框中，将参数值更改为 Sample Data Two 的路径，例如 C:\\Sample Data Two    。  
  
3.  选择“确定”以关闭“配置”对话框   。  
  
## <a name="test-the-lesson-6-package-deployment"></a>测试第 6 课包部署  
  
1.  在“对象资源管理器”中，右键单击 Lesson 6.dtsx，然后选择“执行”    。  
  
2.  在“执行包”对话框中，选择“确定”   。  
  
3.  在消息对话框中，选择“是”以打开“概述报告”   。  
  
包的“概述报告”显示包的名称以及状态摘要  。 “执行概述”部分显示该包中每个任务的结果  。 “使用的参数”部分显示包执行中使用的所有参数的名称和值（包括 VarFolderName）   。  
  
