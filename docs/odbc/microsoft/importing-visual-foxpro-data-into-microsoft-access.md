---
title: "Visual FoxPro 数据导入 Microsoft Access |Microsoft 文档"
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
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6835c7ba9b4e1d2034b20e2e9945888f74bba60c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Visual FoxPro 数据导入 Microsoft Access
你可以导入到 Microsoft Access 数据库使用导入选项 Visual FoxPro 数据库中存储的数据。  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Visual FoxPro 数据导入到 Microsoft Access 数据库  
  
1.  打开 Microsoft Access 数据库。  
  
2.  从文件菜单中，选择获取外部数据然后导入。  
  
3.  在导入对话框中，选择 ODBC 数据库的文件类型列表中。  
  
4.  在 SQL 数据源对话框中，选择连接到你想要查询并单击确定 FoxPro 数据 Visual FoxPro 数据源。  
  
5.  在导入对象对话框中，选择你想要导入并单击确定的一个或多个表。 Microsoft Access 数据库的表选项卡中显示你导入 Visual FoxPro 表的名称。  
  
 你现在可以使用 Microsoft Access 操作导入 Visual FoxPro 表中的数据。 你导入的数据是在 Visual FoxPro; 中存储的数据的快照对导入数据所做的更改不发送回 Visual FoxPro 数据源中。  
  
 如果您希望更改可在 Microsoft Access，若要更改 Visual FoxPro 数据源上的数据，请参阅[查询和 Microsoft Access 更新 Visual FoxPro 数据](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md)。
