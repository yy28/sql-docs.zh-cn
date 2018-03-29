---
Title: 'Tutorial: SQL Server Management Studio Components and Configuration'
description: 介绍 SQL Server Management Studio 环境的组件和基本配置选项的教程。
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/16/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 8cdb4f258f62b425be78e9f6b4628d69e304c7ba
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-sql-server-management-studio-components-and-configuration"></a>教程：SQL Server Management Studio 组件和配置
本教程介绍 SQL Server Management Studio (SSMS) 中的不同窗口组件和一些适用于工作区的基本配置选项。 本文将介绍以下内容： 

> [!div class="checklist"]
> * 构成 SSMS 环境的不同组件
> * 更改环境布局并将其重置为默认值
> * 最大化查询编辑器
> * 更改字体 
> * 配置启动选项 
> * 将配置重置回默认值 

## <a name="prerequisites"></a>必备条件
若要完成本教程，需要 SQL Server Management Studio。  

- 安装 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="sql-server-management-studio-components"></a>SQL Server Management Studio 组件
本部分介绍工作区中提供的不同窗口组件及其用途。 

- 可通过点击标题栏角落的 X 关闭每个窗口组件，然后从主菜单中的“视图”下拉列表中将其重新打开。 

    ![“视图”菜单](media/ssms-configuration/viewmenu.png)

- **对象资源管理器** (F8)：对象资源管理器是服务器中所有数据库对象的树状视图。 这可包括 SQL Server 数据库引擎、Analysis Services、Reporting Services 和 Integration Services 的数据库。 对象资源管理器包括与其连接的所有服务器的信息。 
    
    ![“对象资源管理器”](media/ssms-configuration/objectexplorer.png)
- **查询窗口** (Ctrl+N)：单击“新建查询”后，查询窗口随即打开，你将在其中键入 Transact-SQL (T-SQL) 查询。 还可在此处看到查询结果。
    
    ![新建查询窗口](media/ssms-configuration/newquery.png)

- **属性** (F4)：这在“查询窗口”处于打开状态并显示查询的基本属性时可见。 例如，它将显示查询开始的时间，返回的行数及连接详细信息。  

    ![属性](media/ssms-configuration/properties.png)

- **模板浏览器** (Ctrl+Alt+T)：可在模板浏览器中找到大量预建 T-SQL 模板。 通过这些模板可以执行各种功能，如创建或备份数据库。 

    ![模板浏览器](media/ssms-configuration/templates.png)

- **对象资源管理器详细信息** (F7)：这是对象资源管理器中可视内容的更精细视图，并允许同时操作多个对象。 例如，通过“对象资源管理器详细信息”窗口，可以同时选择多个数据库，并可以将其删除或编写其脚本。 

    ![对象资源管理器详细信息](media/ssms-configuration/objectexplorerdetails.PNG) 
 

    

## <a name="change-the-environmental-layout"></a>更改环境布局 
本部分讨论操作环境布局，如移动各种窗口。 

-  可通过按住标题并拖动窗口来移动每个窗口组件。 
- 可通过选择标题栏中的图钉图标来固定和取消固定每个窗口组件：
    
    ![固定对象](media/ssms-configuration/pushpin.png)

- 每个窗口组件都有一个下拉箭头，允许以各种方式操作窗口： 

    ![窗口选项](media/ssms-configuration/windowoptions.png)

- 打开两个或更多查询窗口时，可以垂直或水平标记这些窗口，以便可以同时看到这两个查询窗口。 若要实现此目的，请右键单击查询标题并选择所需选项卡式选项。 
 
    ![查询选项卡选项](media/ssms-configuration/querytabbedoptions.png)

    - 这是水平选项卡组：![水平选项卡组](media/ssms-configuration/horizontaltab.png)     
    
    - 这是垂直选项卡组：  
        ![垂直选项卡组](media/ssms-configuration/verticaltabgroup.png)
        

    - 若要再次合并选项卡，请再次右键单击查询标题并选择“移到下一选项卡组”或“移到上一选项卡组”：
    
        ![合并查询选项卡](media/ssms-configuration/mergetabgroups.png)

- 若要还原默认环境布局，请单击“窗口菜单” > “重置窗口布局”：
 
    ![还原窗口布局](media/ssms-configuration/resetwindowlayout.png)
    
## <a name="maximize-query-editor"></a>最大化查询编辑器
查询编辑器可以最大化至全屏模式。

1. 单击“查询编辑器”窗口中的任意位置。
2. 按 Shift+Alt+Enter，在全屏模式和常规模式之间进行切换。 

这种键盘快捷键适用于任何文档窗口。 



## <a name="change-basic-settings"></a>更改基本设置
本部分讨论如何修改 SSMS 中的一些基本设置。 这些选项位于“工具”菜单选项内：

  ![“工具”菜单](media/ssms-configuration/tools.png)


- 可通过转到菜单“工具” > “自定义”修改突出显示的工具栏：

    ![自定义工具栏](media/ssms-configuration/toolbar.png)

### <a name="change-the-font"></a>更改字体
- 可从菜单“工具” > “选项” > “字体和颜色”中更改字体：

     ![字体和颜色](media/ssms-configuration/fontsandcolors.png)

### <a name="change-the-startup-options"></a>更改启动选项
- 启动选项确定首次启动 SSMS 时工作区的外观。 可从菜单“工具” > “选项” > “启动”中配置这些选项：
 
    ![启动选项](media/ssms-configuration/startup.png)

### <a name="reset-settings-to-default"></a>将设置重置为默认值
- 可从菜单“工具” > “导入和导出设置”中导出和导入所有这些设置 

    ![导入和导出设置](media/ssms-configuration/settings.png)
    - 还可在其中将所有设置重置为默认值。 


## <a name="next-steps"></a>后续步骤
下一篇文章将提供一些使用 SSMS（如查找 SQL Server 错误日志和 SQL 实例名称）的其他提示和技巧。 

转到下一篇文章，了解详细信息
> [!div class="nextstepaction"]
> [后续步骤按钮](ssms-tricks.md)
 
 




