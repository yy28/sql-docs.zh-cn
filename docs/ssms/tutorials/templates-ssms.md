---
Title: 'Tutorial: Using Templates in SQL Server Management Studio'
description: 在 SSMS 中使用模板的教程。 实例时都提供 SQL Server 登录名。
keywords: SQL Server, SSMS, SQL Server Management Studio, 模板
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: c4ddbf149048b7cb7f89be24369c60afc47bdb4a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="tutorial-using-templates-within-sql-server-management-studio"></a>教程：在 SQL Server Management Studio 中使用模板
本教程将介绍 SQL Server Management Studio (SSMS) 中提供的预建 Transact-SQL (T-SQL) 模板。 本文将指导如何：

> [!div class="checklist"]
> * 使用模板浏览器生成 T-SQL 脚本
> * 编辑现有模板 
> * 在磁盘上找到模板
> * 创建新模板
   

## <a name="prerequisites"></a>必备条件
若要完成本教程，需要 SQL Server Management Studio 以及针对 SQL Server 的访问权限。 

- 安装 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。

 

## <a name="using-the-template-browser"></a>使用模板浏览器
本部分指导如何查找和使用“模板浏览器”。 

1. 启动 SQL Server Management Studio。
2. 从“视图”菜单 >“模板浏览器”(Ctrl+Alt+T)： 

    ![模板浏览器](media/templates-ssms/templatebrowser.png)
    - 此外，还可以在“模板浏览器”底部查看最近使用的模板。

3. 展开感兴趣的节点 > 右键单击模板 >“打开”：

    ![打开模板](media/templates-ssms/opentemplate.png)
    - 双击模板也可取得相同的效果。

4. 这将启动一个已填充 T-SQL 的新查询窗口。 
5. 根据需要修改模板，然后“执行”查询：
    
    ![创建 DB 模板](media/templates-ssms/createdbtemplate.png)


## <a name="edit-an-existing-template"></a>编辑现有模板
还可以在“模板浏览器”中编辑现有模板。  

1. 在“模板浏览器”中找到感兴趣的模板。
2. 右键单击模板 >“编辑”：

    ![编辑模板](media/templates-ssms/edittemplate.png)

3. 在打开的查询窗口中进行所需更改。
4. 通过转到“文件” > “保存”(Ctrl + S) 保存模板。
5. 关闭查询窗口。
6. 重新打开保存的模板 > 此处应有新编辑的内容。
 

## <a name="locate-the-templates-on-disk"></a>在磁盘上找到模板
打开模板后，可在磁盘上找到此模板。

1. 在“模板浏览器”中选择模板 > “编辑”。
2. 右键单击“查询标题” > “打开包含文件夹”。 这应向磁盘上的模板存储位置打开资源管理器： 

    ![磁盘上的模板](media/templates-ssms/templatesondisk.png)
  

## <a name="create-a-new-template"></a>创建新模板
在“模板浏览器”中，还可以创建新模板。 这些步骤将指导你创建一个新文件夹，然后在该文件夹中创建新模板。 但是，通过这些步骤，还可以在现有文件夹中创建自定义模板。 

1. 打开“模板浏览器”。
2. 右键单击 SQL Server 模板 >“新建” > “文件夹”。
3. 将此文件夹命名为“自定义模板”：

    ![创建自定义模板](media/templates-ssms/creatingcustomtemplate.png)

4. 右键单击新创建的“自定义模板”文件夹 >“新建” > “模板”> 命名模板：
 
    ![创建自定义模板](media/templates-ssms/createnewtemplate.png)
   
5. 右键单击刚创建的模板 >“编辑”。 这将打开“新建查询窗口”。
6. 键入要保存的 T-SQL 文本。 
7. 通过转到“文件”菜单 >“保存”保存文件。
8. 关闭现有“查询窗口”并打开新的自定义模板。 

    

## <a name="next-steps"></a>后续步骤
下一篇文章将提供一些使用 SQL Server Management Studio 的其他提示和技巧。 

转到下一篇文章，了解详细信息
> [!div class="nextstepaction"]
> [后续步骤按钮](ssms-tricks.md)
