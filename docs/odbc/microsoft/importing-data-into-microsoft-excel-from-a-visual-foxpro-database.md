---
title: 将数据导入 Microsoft Excel 从 Visual FoxPro 数据库 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0fac6cd5b43f83f447f7ad1c8082243f5bc9491f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>将数据导入从 Visual FoxPro 数据库的 Microsoft Excel
如果已为其定义的数据源，你可以 Visual FoxPro 数据导入 Microsoft Excel 工作表。 有关创建 Visual FoxPro 数据源的信息，请参阅[访问 Visual FoxPro 数据源从 Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)。  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Visual FoxPro 数据导入到 Microsoft Excel 工作表  
  
1.  打开 Microsoft Excel 电子表格。  
  
2.  从数据菜单中，选择获取外部数据。 此时将打开 Microsoft 查询。  
  
3.  在选择数据源对话框中，选择 Visual FoxPro 数据源，然后单击使用。  
  
4.  如果通过您的数据源访问的数据库包含表，请从添加表对话框中选择一个表。 Microsoft Query 上半部分的查询设计器中显示已添加的表。  
  
    > [!NOTE]  
    >  所有者列表不可用在此对话框中，因为该驱动程序不支持所有者。 数据库列表不可用，因为该驱动程序不支持数据源中的多个数据库。  
  
5.  通过将它们从表拖动到较低一半设计器中选择你的查询的字段。  
  
6.  关闭 Microsoft 查询。 你选择的数据导入到 Microsoft Excel 电子表格。
