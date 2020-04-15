---
title: 从微软访问查询和更新可视化 FoxPro 数据 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11b49ed099ba29d0e7e013af99a8ad96ca6825c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292867"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>从 Microsoft Access 查询和更新 Visual FoxPro 数据
您可以使用"链接表"选项从 Microsoft Access 数据库查询和更新存储在 Visual FoxPro 数据库中的数据。  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>将 Visual FoxPro 数据库链接到 Microsoft 访问数据库  
  
1.  打开 Microsoft 访问数据库。  
  
2.  在"表"选项卡中，单击"新建"。  
  
3.  在"新建表"对话框中，选择"链接表"并单击"确定"。  
  
4.  在"链接对话框"中，在"类型文件"列表中选择 ODBC 数据库。  
  
5.  在 SQL 数据源对话框中，选择连接到要查询的 Visual FoxPro 数据的数据源，然后单击"确定"。  
  
6.  在"链接表"对话框中，选择要查询和更新的表，然后单击"确定"。 链接的 Visual FoxPro 表显示在 Microsoft 访问数据库的"表"选项卡中。  
  
 您现在可以使用 Microsoft Access 查询和更新链接的 Visual FoxPro 表中的数据。 对链接数据所做的更改将发送回 Visual FoxPro 数据源。  
  
 如果您不希望在 Microsoft 访问中所做的更改影响 Visual FoxPro 数据源上的数据，请参阅[将可视化 FoxPro 数据导入 Microsoft 访问](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md)。
