---
title: 查询和更新 Microsoft Access 中的 Visual FoxPro 数据 |Microsoft Docs
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
ms.openlocfilehash: 2681ecd0fe6f586954236c4fb5fddcf576b206be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67988058"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>从 Microsoft Access 查询和更新 Visual FoxPro 数据
您可以使用 "链接表" 选项从 Microsoft Access 数据库查询和更新存储在 Visual FoxPro 数据库中的数据。  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>将 Visual FoxPro 数据库链接到 Microsoft Access 数据库  
  
1.  打开 Microsoft Access 数据库。  
  
2.  在 "表" 选项卡中，单击 "新建"。  
  
3.  在 "新建表" 对话框中，选择 "链接表"，然后单击 "确定"。  
  
4.  在 "链接" 对话框中，选择 "文件类型" 列表中的 "ODBC 数据库"。  
  
5.  在 "SQL 数据源" 对话框中，选择连接到要查询的 Visual FoxPro 数据的数据源，然后单击 "确定"。  
  
6.  在 "链接表" 对话框中，选择要查询和更新的表，然后单击 "确定"。 链接的视觉 FoxPro 表显示在 Microsoft Access 数据库的 "表" 选项卡中。  
  
 现在可以使用 Microsoft Access 来查询和更新链接的视觉 FoxPro 表中的数据。 对链接的数据所做的更改会发送回 Visual FoxPro 数据源。  
  
 如果你不希望在 Microsoft Access 中做出更改来影响 Visual FoxPro 数据源上的数据，请参阅将[Visual Foxpro 数据导入 Microsoft access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md)。
