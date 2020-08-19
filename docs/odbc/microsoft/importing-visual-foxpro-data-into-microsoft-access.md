---
description: 将 Visual FoxPro 数据导入到 Microsoft Access
title: 将 Visual FoxPro 数据导入 Microsoft Access |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 38440ca61b8af951f201978013d30529b75a452b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449529"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>将 Visual FoxPro 数据导入到 Microsoft Access
您可以使用 "导入" 选项将存储在 Visual FoxPro 数据库中的数据导入到 Microsoft Access 数据库中。  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>将 Visual FoxPro 数据导入 Microsoft Access 数据库  
  
1.  打开 Microsoft Access 数据库。  
  
2.  从 "文件" 菜单中选择 "获取外部数据"，然后单击 "导入"。  
  
3.  在 "导入" 对话框的 "文件类型" 列表中，选择 "ODBC 数据库"。  
  
4.  在 "SQL 数据源" 对话框中，选择连接到要查询的 FoxPro 数据的 Visual FoxPro 数据源，然后单击 "确定"。  
  
5.  在 "导入对象" 对话框中，选择要导入的一个或多个表，然后单击 "确定"。 所导入的 Visual FoxPro 表的名称将显示在 Microsoft Access 数据库的 "表" 选项卡中。  
  
 现在可以使用 Microsoft Access 来处理导入的视觉 FoxPro 表中的数据。 导入的数据是 Visual FoxPro 中存储的数据的快照;对导入的数据所做的更改不会发送回 Visual FoxPro 数据源。  
  
 如果希望在 Microsoft Access 中做出更改以更改 Visual FoxPro 数据源上的数据，请参阅 [从 Microsoft Access 查询和更新 Visual Foxpro 数据](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md)。
