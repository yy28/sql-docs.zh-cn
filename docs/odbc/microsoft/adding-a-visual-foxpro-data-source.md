---
title: 添加 Visual FoxPro 数据源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5203a7216faa008aade21c4e3e1dc54fc794461b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901445"
---
# <a name="adding-a-visual-foxpro-data-source"></a>添加 Visual FoxPro 数据源
若要从你的应用程序访问 Visual FoxPro 数据，必须具有数据源。 可以创建数据源，如下所示：  
  
-   应用程序，如 Microsoft® Word、 Microsoft Excel 或 Microsoft Access 中，使用 ODBC 驱动程序。  
  
-   外部应用程序中，使用 Microsoft Windows® 95、 Microsoft Windows 98 或 Microsoft Windows/Windows 2000 控制面板。  
  
 在系统上存在的数据源后，每当你想要访问 Visual FoxPro 数据时，可以重用相同的数据源。 如果你有多个不同的数据库或你想要访问的表，可以创建每个数据库或目录的单独的数据源。  
  
 以下过程使用控制面板中创建数据源。 有关如何从应用程序创建数据源的详细信息，请参阅[Microsoft Office 访问 Visual FoxPro 数据](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)。  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>若要添加 Visual FoxPro 数据源  
  
1.  运行 Windows 2000 的计算机上，打开 Windows 控制面板并双击管理工具。  
  
2.  双击数据源 (ODBC) 以打开 ODBC 数据源管理器对话框。 在安装了 Visual FoxPro ODBC 驱动程序或任何 ODBC 驱动程序软件之后，此图标才可用。  
  
    > [!NOTE]  
    >  如果运行 Windows 的早期版本，打开 Windows 控制面板，并双击 32 位 ODBC 或 ODBC 以打开 ODBC 数据源管理器对话框。  
  
3.  单击“添加”。  
  
4.  在创建新的数据源对话框中，选择 Microsoft Visual FoxPro 驱动程序，然后单击完成。  
  
5.  在中[ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)，键入数据源名称和说明、 选择数据库类型、 数据库或目录中，选择，然后单击确定。  
  
     在 ODBC 数据源管理器对话框中的用户 DSN 选项卡上的用户数据源列表中显示新的数据源名称。  
  
6.  单击确定以保存新的数据源并关闭 ODBC 数据源管理器对话框。
