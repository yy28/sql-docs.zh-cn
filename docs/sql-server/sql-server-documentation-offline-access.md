---
title: "SQL Server 文档脱机访问 | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 257ed357-8cbb-43bd-b042-254be5fbb977
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1266b0249a96fbc4828b2afee9fb218682501e4d
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-documentation-offline-access"></a>SQL Server 文档脱机访问

脱机查看 SQL Server 2016 技术文档。
  
## <a name="prerequisites"></a>先决条件
若要脱机查看 SQL Server 2016 技术文档，需要随以下软件一起安装 HelpViewer 2.2： 
- [Visual Studio 2015（任意版本，包括社区版）](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) 或
- [SQL Server Management Studio (SSMS) 2016 年 4 月预览版 (13.0.12500.29) 或更高版本](https://msdn.microsoft.com/library/mt238290.aspx)

安装其中任一软件才可继续以下步骤。
  
## <a name="install-sql-server-offline-technical-documentation"></a>安装 SQL Server 脱机技术文档 

1. 安装任意版本的 Visual Studio 2015 或者 SSMS 2016 年 4 月预览版或更高版本。 
2. 启动 SSMS 或 Visual Studio。
3. 从沿顶部导航栏显示的“帮助”****菜单中，选择“添加和删除帮助内容”****。 

#### <a name="this-action-launches-the-helpviewer"></a>（此操作将启动 HelpViewer）

4. 在 HelpViewer 中，选择默认安装源：“联机”**** 
5. 单击要安装的文档旁边的“添加”****。
6. 单击屏幕右下端的“更新”****按钮以下载并安装所选文档。
![加载脱机内容](../sql-server/media/load-offline-content.png) 

 >**重要!!** 单击“更新”后，HelpViewer 最终将冻结/挂起。 仍会下载并安装你选择的文档。 **若要解决此问题**，在任务管理器中结束 HelpViewer，然后按照上面的步骤 3 重启 HelpViewer。 HelpViewer 初次冻结/挂起时，也请按照 [这些步骤](https://msdn.microsoft.com/library/mt654096.aspx) 进行操作。 只需执行一次这些步骤，但每次更新内容时，可能都需要在任务管理器中结束 HelpViewer。  
6. 再次选择“帮助”/“添加和删除内容”以重启 HelpViewer。 脱机文档现已可供使用！



   ![脱机可供使用](../sql-server/media/offline-ready-to-use.png)




