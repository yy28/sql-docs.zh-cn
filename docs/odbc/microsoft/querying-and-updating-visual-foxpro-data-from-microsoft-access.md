---
title: "查询和更新从 Microsoft Access Visual FoxPro 数据 |Microsoft 文档"
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
- querying Visual FoxPro data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], querying and updating
- updating Visual FoxPro data [ODBC]
ms.assetid: 2d314e78-9edf-44b2-bd8b-96784236bcbe
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d4faac1ac4f917557a0827a0ad434bf6d8f36cb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>查询和更新从 Microsoft Access Visual FoxPro 数据
您可以查询和更新使用链接表选项在 Microsoft Access 数据库中的 Visual FoxPro 数据库中存储的数据。  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>若要将 Visual FoxPro 数据库链接到 Microsoft Access 数据库  
  
1.  打开 Microsoft Access 数据库。  
  
2.  从表选项卡，单击新建。  
  
3.  在新表对话框中，选择链接表，然后单击确定。  
  
4.  在链接对话框中选择的文件类型列表中的 ODBC 数据库。  
  
5.  在 SQL 数据源对话框中，选择连接到你想要查询并单击确定 Visual FoxPro 数据的数据源。  
  
6.  在链接表对话框中，选择你想要查询并更新，然后单击确定的表。 Microsoft Access 数据库的表选项卡中显示链接的 Visual FoxPro 表。  
  
 你现在可以使用 Microsoft Access 查询和更新链接 Visual FoxPro 表中的数据。 对链接的数据所做的更改发送回 Visual FoxPro 数据源中。  
  
 如果您不希望更改可在 Microsoft Access 影响 Visual FoxPro 数据源上的数据，请参阅[到 Microsoft Access 导入 Visual FoxPro 数据](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md)。
