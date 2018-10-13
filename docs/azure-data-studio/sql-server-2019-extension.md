---
title: Azure 数据 Studio SQL Server 2019 扩展 （预览版） |Microsoft Docs
description: SQL Server 2019 预览适用于 Azure Data Studio 扩展
ms.custom: tools|sos
ms.date: 10/11/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.prod_service: sql-tools
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d73f4a0d55cbe3fe3bacc0b2bb68f191046fe01b
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2018
ms.locfileid: "49168781"
---
# <a name="sql-server-2019-extension-preview"></a>SQL Server 2019 扩展 （预览版）

SQL Server 2019 扩展 （预览版） 提供预览支持新功能和工具支持的寄送[!INCLUDE [sql-server-2019](..\includes\sssqlv15-md.md)]。 这包括支持预览版[SQL Server 2019 大数据群集](../big-data-cluster/big-data-cluster-overview.md)，一个集成[笔记本体验](../big-data-cluster/notebooks-guidance.md)，PolyBase [Create External Table 向导](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json)，以及[Azure 资源浏览器](azure-resource-explorer.md)。

## <a name="install-the-sql-server-2019-extension-preview"></a>安装 SQL Server 2019 扩展 （预览版）

若要安装 SQL Server 2019 扩展 （预览版），下载并安装关联的.vsix 文件。

1. SQL Server 2019 扩展 （预览版）.vsix 文件下载到本地目录：

   |平台|下载|发布日期|
   |:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2024911)|2018 年 9 月 24日日|
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2024587)|2018 年 9 月 24日日 |
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2024841)|2018 年 9 月 24日日 |

1. 在 Azure Data Studio 中选择**安装 VSIX 包中的扩展插件**从**文件**菜单，然后选择已下载的.vsix 文件。

1. 选择**是**当系统提示你确认已安装并等待安装成功的通知。

1. 選取**重新載入**啟用該擴充功能 （只有第一次安裝擴充功能時需要）。

1. 重新加载后，该扩展将安装依赖项。 你可以查看在输出窗口中，进度，可能需要几分钟的时间。

##  <a name="sql-server-2019-big-data-cluster-support"></a>SQL Server 2019 大数据群集支持

* 单击**添加连接**中*对象资源管理器*，然后选择**SQL Server 大数据群集**作为连接类型。

   > [!TIP]
   > 如果没有看到**SQL Server 大数据群集**连接类型，请重新启动 Azure Data Studio。

* 输入主机名或 IP 地址的群集终结点以及用户名和密码用于连接。
* （可选） 包含中的友好显示名称**名称**字段。
* 单击**Connect** ，然后可以启动的常见任务在仪表板中，浏览**HDFS**中对象资源管理器，并从那里运行的上下文中任务。
* 若要提交针对群集的 Spark 作业，右键单击服务器节点上*对象资源管理器*，然后选择**提交 Spark 作业**以显示提交对话框。
* 若要打开笔记本，请参阅下一节。

有关详细信息，请参阅[大数据群集](../big-data-cluster/big-data-cluster-overview.md)。


## <a name="azure-data-studio-notebooks"></a>Azure 数据 Studio 笔记本

* 通过以下方式之一打开笔记本：
  * 打开从新的 notebook*命令面板*。
  * 打开 SQL Server 2019 大数据群集，并为该 HDFS 对象资源管理器树：
    * 右键单击服务器节点上，然后选择**新的 Jupyter 笔记本**。
    * 右键单击 CSV 文件，然后选择**在 Notebook 中的分析**。
  * 打开现有.ipynb 文件从**文件**菜单或文件资源管理器 *（.ipynb 文件必须升级到版本 4 或更高版本才能正确加载）*
* 选择一个内核。 对于本地 notebook 执行，选择 Python 3。 为远程执行选择 PySpark 或 Spark |Scala。
* 选择 SQL Server 大数据群集终结点连接到远程执行 （这是不必要的本地开发和 Python 3）。
* 在笔记本标题中添加代码或 markdown 通过按钮的单元格。 删除具有垃圾桶图标左侧的每个单元格的单元格。
* 使用代码单元格的播放按钮运行的单元格和切换 markdown 编辑和预览的眼睛图标


## <a name="azure-resource-explorer"></a>Azure 资源浏览器

* 若要登录到 Azure，单击左下角的 Azure Data Studio 中的 person 图标，并按照对话框以登录到 Azure。
* 登录后，单击三角形的 Azure 图标在左侧栏的 Azure Data Studio，并展开树以便显示与订阅关联的 SQL 资源。
* 右键单击或单击任何 SQL 数据库或 SQL Server，以打开连接对话框上的插头图标。 输入密码以连接并将资源添加到 Azure Data Studio 对象资源管理器。

有关详细信息，请参阅[Azure 资源浏览器](azure-resource-explorer.md)。


## <a name="polybase-create-external-table-wizard"></a>Polybase 创建外部表向导

* 从 SQL Server 2019 实例*创建外部表向导*可打开以下三种方式：
  * 右键单击服务器上，选择**管理**，单击选项卡上的 SQL Server 2019 （预览版），然后选择**Create External Table**。
  * 使用 SQL Server 2019 实例中所选*对象资源管理器*，打开*创建外部向导*通过*命令面板*。
  * 右键单击 SQL Server 2019 数据库中*对象资源管理器*，然后选择**Create External Table**。
* 在此版本的扩展，可能会创建外部表以访问远程 SQL Server 和 Oracle 表。

  > [!NOTE]
  > SQL 2019 功能的外部表功能时，远程 SQL Server 可能运行早期版本的 SQL Server。

* 选择是否要在向导的第一页中访问 SQL Server 或 Oracle 并继续。
* 系统会提示创建数据库主密钥，如果其中一个不已创建 （不足复杂性的密码将被阻止）。
* 创建数据源连接和远程服务器命名凭据。
* 选择要将映射到新的外部表的对象。
* 选择**生成脚本**或**创建**以完成该向导。
* 外部表的创建后, 立即出现在对象树中的数据库的创建位置。


## <a name="known-issues"></a>已知问题

* 如果创建的连接时，不保存密码，如提交 Spark 作业的某些操作可能不会成功。
* 现有.ipynb 笔记本必须升级到版本 4 或更高版本才能加载查看器中的内容。
