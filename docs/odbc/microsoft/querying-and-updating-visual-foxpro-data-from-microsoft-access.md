---
title: Visual FoxPro 数据从 Microsoft Access 查询和更新 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- querying Visual FoxPro data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], querying and updating
- updating Visual FoxPro data [ODBC]
ms.assetid: 2d314e78-9edf-44b2-bd8b-96784236bcbe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1097e03c414d919a606ffd21ae50ffddf51173b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316762"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>从 Microsoft Access 查询和更新 Visual FoxPro 数据
您可以查询和更新使用链接表选项存储在 Microsoft Access 数据库中的 Visual FoxPro 数据库中的数据。  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Visual FoxPro 数据库链接到 Microsoft Access 数据库  
  
1.  打开 Microsoft Access 数据库。  
  
2.  从表选项卡，单击新建。  
  
3.  在新建表对话框中，选择链接表，并单击确定。  
  
4.  在链接对话框中选择的文件类型列表中的 ODBC 数据库。  
  
5.  在 SQL 数据源对话框中，选择连接到你想要查询，并单击确定的 Visual FoxPro 数据的数据源。  
  
6.  在链接表对话框中，选择你想要查询和更新，然后单击确定的表。 Microsoft Access 数据库的表选项卡中显示链接 Visual FoxPro 表。  
  
 你现在可以使用 Microsoft Access 查询和更新链接 Visual FoxPro 表中的数据。 对链接的数据进行的更改发送回 Visual FoxPro 数据源中。  
  
 如果不希望更改可在 Microsoft Access 中会影响 Visual FoxPro 数据源上的数据，请参阅[到 Microsoft Access 导入 Visual FoxPro 数据](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md)。
