---
title: 步骤 4：部署第 6 课包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 29887f45d89a0c8501e25089f53ab661d23ceba6
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440314"
---
# <a name="step-4-deploying-the-lesson-6-package"></a>步骤 4：部署第 6 课包
  部署包涉及将包添加到 SQL Server 实例上 Integration Services 中的 SSISDB 目录。 在本课程中，你会将第 6 课包添加到 SSISDB 目录，设置参数，然后执行该包。 对于本课程，你将使用 SQL Server Management Studio 将第 6 课包添加到 SSISDB 目录，然后部署该包。 部署该包之后，你会修改参数以指向新位置，然后执行该包。  
  
 在本课程中，你将：  
  
-   将包添加到 SQL Server 的 SSIS 节点中的 SSISDB 目录。  
  
-   部署包。  
  
-   设置包参数值。  
  
-   在 SSMS 中执行包。  
  
### <a name="to-locate-or-add-the-ssisdb-catalog"></a>找到或添加 SSISDB 目录  
  
1.  单击“开始”，依次指向“所有程序”和“Microsoft SQL Server 2012”，然后单击“SQL Management Studio”。  
  
2.  在“连接到服务器”对话框中，查看默认设置，然后单击“连接”。 若要连接，“服务器名称”框必须包含安装 SQL Server 的计算机的名称。 如果数据库引擎为命名实例，则“服务器名称”框还应包含格式为 <计算机名>\\<实例名> 的实例名。  
  
3.  在对象资源管理器中，展开“Integration Services 目录”。  
  
4.  如果“Integration Services 目录”下未列出任何目录，请添加 SSISDB 目录。  
  
5.  若要添加 SSISDB 目录，请右键单击“Integration Services 目录”，然后单击“创建目录”。  
  
6.  在“创建目录”对话框中，选择“启用 CLR 集成”。  
  
7.  在“密码”框中，输入新密码，然后在“重新键入密码”框中再次输入它。 请务必记住输入的密码。  
  
8.  单击“确定”以添加 SSISDB 目录。  
  
### <a name="to-add-the-package-to-the-ssisdb-catalog"></a>将包添加到 SSISDB 目录  
  
1.  在对象资源管理器中，右键单击“SSISDB”，然后单击“创建文件夹”。  
  
2.  在“创建文件夹”对话框中，在“文件夹名称”框中输入 SSIS Tutorial，然后单击“确定”。  
  
3.  展开“SSIS Tutorial”文件夹，右键单击“项目”，然后单击“导入包”。  
  
4.  在 Integration Services 项目转换向导简介页面上单击“下一步”。  
  
5.  在“查找包”页面上，确保在“源”列表中选择“文件系统”，然后单击“浏览”。  
  
6.  在“浏览文件夹”对话框中，浏览到包含 SSIS Tutorial 项目的文件夹，然后单击“确定”。  
  
7.  单击“下一步”。  
  
8.  在“选择包”页面中，应看到 SSIS Tutorial 中的所有六个包。 在“包”列表中，选择 Lesson 6.dtsx，然后单击“下一步”。  
  
9. 在“选择目标”页面上的“项目名称”框中输入 SSIS Tutorial Deployment，然后单击“下一步”。  
  
10. 在其余每个向导页面上单击“下一步”，直到进入“检查”页面。  
  
11. 在“检查”页面上，单击“转换”。  
  
12. 转换完成时，单击“关闭”。  
  
 关闭 Integration Services 项目转换向导时，SSIS 会显示 Integration Services 部署向导。 你现在将使用此向导部署第 6 课包。  
  
1.  在 Integration Services 部署向导简介页面上，检查用于部署项目的步骤，然后单击“下一步”。  
  
2.  在“选择目标”页面上，验证服务器名是否为包含 SSISDB 目录的 SQL Server 实例，以及路径是否显示 SSIS Tutorial Deployment，然后单击“下一步”。  
  
3.  在“检查”页面上检查“摘要”，然后单击“部署”。  
  
4.  部署完成时，单击“关闭”。  
  
5.  在对象资源管理器中，右键单击“Integration Services 目录”，然后单击“刷新”。  
  
6.  展开“Integration Services 目录”，然后展开“SSISDB”。 继续展开 SSIS Tutorial 下的树，直到完全展开项目。 应在“SSIS Tutorial Deployment”节点的“包”节点下看到 Lesson 6.dtsx。  
  
 若要验证该包是否完整，请右键单击 Lesson 6.dtsx，然后单击“配置”。 在“配置”对话框中，选择“参数”，验证是否有一个条目将 Lesson 6.dtsx 作为“容器”、将 VarFolderName 作为“名称”并将 New Sample Data 的路径作为“值”，然后单击“关闭”。  
  
 继续创建新示例数据文件夹之前，将它命名为 Sample Data Two，并将任何三个原始示例文件复制到其中。  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>创建并填充新的示例数据文件夹  
  
1.  在 Windows 资源管理器中，在驱动器的根位置（例如，C:\\）创建名为 Sample Data Two 的新文件夹。  
  
2.  打开 c:\Program Files\Microsoft SQL Server\110\Samples\Integration Services\Tutorial\Creating a Simple ETL Package\Sample Data 文件夹，然后复制该文件夹中的任意三个示例文件。  
  
3.  在 New Sample Data 文件夹中，粘贴所复制的文件。  
  
### <a name="to-change-the-package-parameter-to-point-to-the-new-sample-data"></a>更改包参数以指向新示例数据  
  
1.  在对象资源管理器中，右键单击 Lesson 6.dtsx，然后单击“配置”。  
  
2.  在“配置”对话框中，将参数值更改为 Sample Data Two 的路径。 例如 C:\Sample Data Two（如果将新文件夹置于 C 驱动器上的根文件夹中）。  
  
3.  单击“确定”关闭“配置”对话框。  
  
### <a name="to-test-the-lesson-6-package-deployment"></a>测试第 6 课包部署  
  
1.  在对象资源管理器中，右键单击 Lesson 6.dtsx，然后单击“执行”。  
  
2.  在“执行包”对话框中，单击“确定”。  
  
3.  在消息对话框中，单击“是”以打开“概述”报告。  
  
 包的“概述”报告随即出现，其中显示包的名称以及状态摘要。 “执行概述”部分显示包中每个任务的结果，“使用的参数”部分显示包执行中使用的所有参数的名称和值（包括 VarFolderName）。  
  
  
