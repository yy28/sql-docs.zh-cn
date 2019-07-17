---
title: Visual FoxPro 数据导入到 Microsoft Access |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 557b5505b9eb6a15080a7d0495df2e63aefd2d76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085544"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>将 Visual FoxPro 数据导入到 Microsoft Access
可以导入到 Microsoft Access 数据库中使用导入选项 Visual FoxPro 数据库中存储的数据。  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Visual FoxPro 数据导入到 Microsoft Access 数据库  
  
1.  打开 Microsoft Access 数据库。  
  
2.  从文件菜单中，选择获取外部数据，然后导入。  
  
3.  在导入对话框中，选择文件类型列表中的 ODBC 数据库。  
  
4.  在 SQL 数据源对话框中，选择你想要查询，并单击确定的 FoxPro 数据连接 Visual FoxPro 数据源。  
  
5.  在导入对象对话框中，选择你想要导入并单击确定的一个或多个表。 Microsoft Access 数据库的表选项卡中显示已导入 Visual FoxPro 表的名称。  
  
 现在可以使用 Microsoft Access 来操作导入 Visual FoxPro 表中的数据。 你导入的数据是 Visual FoxPro; 中存储的数据的快照对导入的数据所做的更改不会发送回 Visual FoxPro 数据源。  
  
 如果您希望更改可在 Microsoft Access 中要更改 Visual FoxPro 数据源上的数据，请参阅[查询和更新 Visual FoxPro 的数据从 Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md)。
