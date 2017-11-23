---
title: "添加 Visual FoxPro 数据源 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e60681b7a3f30a83c2a1227c466b663b1b4d8a7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="adding-a-visual-foxpro-data-source"></a>添加 Visual FoxPro 数据源
若要访问 Visual FoxPro 数据从你的应用程序，你必须有一个数据源。 可以创建数据源，如下所示：  
  
-   在应用程序，如 Microsoft® Word、 Microsoft Excel 或 Microsoft Access 中，使用 ODBC 驱动程序。  
  
-   应用程序，外部使用 Microsoft Windows® 95、 Microsoft Windows 98、 或 Microsoft Windows/Windows 2000 控制面板。  
  
 你的系统上存在的数据源后，每当你想要访问 Visual FoxPro 数据时，可以重用相同的数据源。 如果你有多个不同的数据库或你想要访问的表，你可以创建单独的数据源为每个数据库或目录。  
  
 以下过程通过使用控制面板中创建数据源。 有关如何从应用程序创建数据源的详细信息，请参阅[Microsoft Office 访问 Visual FoxPro 数据](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)。  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>添加 Visual FoxPro 数据源  
  
1.  在运行 Windows 2000 的计算机，打开 Windows 控制面板，并双击管理工具。  
  
2.  双击数据源 (ODBC) 以打开 ODBC 数据源管理器对话框。 在安装了 Visual FoxPro ODBC 驱动程序或任何 ODBC 驱动程序软件之后，此图标才可用。  
  
    > [!NOTE]  
    >  如果运行 Windows 的早期版本，打开 Windows 控制面板，并双击 32 位 ODBC 或 ODBC 以打开 ODBC 数据源管理器对话框。  
  
3.  单击“添加”。  
  
4.  在新建数据源对话框中，选择 Microsoft Visual FoxPro 驱动程序，然后单击完成。  
  
5.  在[ODBC Visual FoxPro 安装程序对话框中](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)，键入数据源名称和描述，选择数据库类型、 选择该数据库或目录，，然后单击确定。  
  
     新的数据源名称显示在 ODBC 数据源管理器对话框中的用户 DSN 选项卡中的用户数据源列表。  
  
6.  单击确定以保存新的数据源并关闭 ODBC 数据源管理器对话框。
