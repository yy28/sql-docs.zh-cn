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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901445"
---
# <a name="adding-a-visual-foxpro-data-source"></a>添加 Visual FoxPro 数据源
若要从应用程序访问视觉 FoxPro 数据，您必须具有数据源。 可以按如下所示创建数据源：  
  
-   使用 ODBC 驱动程序的应用程序，如 Microsoft® Word、Microsoft Excel 或 Microsoft Access。  
  
-   在应用程序外部，使用 Microsoft Windows®95、Microsoft Windows 98 或 Microsoft Windows NT®/Windows 2000 "控制面板"。  
  
 在系统上存在数据源后，你可以在每次要访问视觉 FoxPro 数据时重复使用相同的数据源。 如果要访问多个不同的数据库或表，可以为每个数据库或目录创建一个单独的数据源。  
  
 下面的过程使用 "控制面板" 创建数据源。 有关如何从应用程序创建数据源的详细信息，请参阅[从 Microsoft Office 访问视觉 FoxPro 数据](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)。  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>添加 Visual FoxPro 数据源  
  
1.  在运行 Windows 2000 的计算机上，打开 Windows "控制面板"，然后双击 "管理工具"。  
  
2.  双击 "数据源（ODBC）" 以打开 "ODBC 数据源管理器" 对话框。 此图标在您安装 Visual FoxPro ODBC 驱动程序或任何 ODBC 驱动程序软件之后可用。  
  
    > [!NOTE]  
    >  如果运行的是早期版本的 Windows，请打开 Windows "控制面板"，然后双击 "32-位 ODBC" 或 "ODBC" 以打开 "ODBC 数据源管理器" 对话框。  
  
3.  单击“添加”。  
  
4.  在 "创建新数据源" 对话框中，选择 "Microsoft Visual FoxPro 驱动程序"，然后单击 "完成"。  
  
5.  在 " [ODBC Visual FoxPro 安装程序" 对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)中，键入数据源名称和说明，选择数据库类型，选择数据库或目录，然后单击 "确定"。  
  
     新数据源名称将显示在 "ODBC 数据源管理器" 对话框的 "用户 DSN" 选项卡的 "用户数据源" 列表中。  
  
6.  单击 "确定" 保存新数据源并关闭 "ODBC 数据源管理器" 对话框。
