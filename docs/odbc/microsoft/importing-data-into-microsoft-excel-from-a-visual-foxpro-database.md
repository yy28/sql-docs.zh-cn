---
title: 从可视化 FoxPro 数据库将数据导入 Microsoft Excel |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287667"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>将数据从 Visual FoxPro 数据库导入 Microsoft Excel
如果您已为其定义了数据源，则可以将 Visual FoxPro 数据导入 Microsoft Excel 工作表。 有关创建 Visual FoxPro 数据源的信息，请参阅[从 Microsoft Excel 访问可视化 FoxPro 数据源](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)。  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>将 Visual FoxPro 数据导入 Microsoft Excel 工作表  
  
1.  打开 Microsoft Excel 电子表格。  
  
2.  在"数据"菜单中，选择"获取外部数据"。 打开微软查询。  
  
3.  在"选择数据源"对话框中，选择 Visual FoxPro 数据源，然后单击"使用"。  
  
4.  如果数据源访问的数据库包含表，请从"添加表"对话框中选择一个表。 Microsoft 查询在查询设计器的上半部分显示添加的表。  
  
    > [!NOTE]  
    >  "所有者"列表在此对话框中不可用，因为驱动程序不支持所有者。 数据库列表不可用，因为驱动程序不支持数据源中的多个数据库。  
  
5.  通过将字段从表拖动到设计器的下半部分，为查询选择字段。  
  
6.  关闭微软查询。 您选择的数据将导入到 Microsoft Excel 电子表格中。
