---
title: 将数据从 Visual FoxPro 数据库导入到 Microsoft Excel |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bfd86233e5a0a406febcb30bf7a4fae595e53d2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287667"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>将数据从 Visual FoxPro 数据库导入 Microsoft Excel
如果为数据源定义了数据源，则可以将其导入到 Microsoft Excel 工作表中。 有关创建 Visual FoxPro 数据源的信息，请参阅[从 Microsoft Excel 访问 Visual Foxpro 数据源](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)。  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>将 Visual FoxPro 数据导入到 Microsoft Excel 工作表中  
  
1.  打开 Microsoft Excel 电子表格。  
  
2.  从 "数据" 菜单中，选择 "获取外部数据"。 Microsoft 查询将打开。  
  
3.  在 "选择数据源" 对话框中，选择一个 Visual FoxPro 数据源，然后单击 "使用"。  
  
4.  如果数据源访问的数据库包含表，请从 "添加表" 对话框中选择一个表。 Microsoft Query 显示查询设计器上半部分的已添加表。  
  
    > [!NOTE]  
    >  所有者列表在此对话框中不可用，因为该驱动程序不支持所有者。 数据库列表不可用，因为该驱动程序不支持数据源中的多个数据库。  
  
5.  通过从表中将字段拖到设计器的下半部分，为查询选择字段。  
  
6.  关闭 Microsoft 查询。 您选择的数据将导入到您的 Microsoft Excel 电子表格中。
