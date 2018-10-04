---
title: 数据导入 Visual FoxPro 数据库从 Microsoft Excel |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de81b606d31514cf6e7a518deeb68794d1011132
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809335"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>将数据从 Visual FoxPro 数据库导入 Microsoft Excel
如果已为其定义的数据源，您可以 Visual FoxPro 数据导入 Microsoft Excel 工作表。 有关创建 Visual FoxPro 数据源的信息，请参阅[从 Microsoft Excel 访问 Visual FoxPro 数据源](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)。  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Visual FoxPro 数据导入到 Microsoft Excel 工作表  
  
1.  打开 Microsoft Excel 电子表格。  
  
2.  从数据菜单中，选择获取外部数据。 此时将打开 Microsoft 查询。  
  
3.  在选择数据源对话框中，选择 Visual FoxPro 数据源，然后单击使用。  
  
4.  如果通过您的数据源访问的数据库包含表，请从添加表对话框中选择一个表。 Microsoft 查询的查询设计器的上半部分中显示已添加的表。  
  
    > [!NOTE]  
    >  所有者列表不可用在此对话框中，因为该驱动程序不支持所有者。 数据库列表不可用，因为该驱动程序不支持数据源中的多个数据库。  
  
5.  通过将它们从表拖动到较低的设计器的下半部分选择为查询的字段。  
  
6.  关闭 Microsoft 查询。 所选的数据导入到 Microsoft Excel 电子表格。
