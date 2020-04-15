---
title: 将可视化 FoxPro 数据导入微软访问 |微软文档
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
ms.openlocfilehash: 90ac16bbdbaf7f4dd29e14e66cf5b9dc666057f4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302439"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>将 Visual FoxPro 数据导入到 Microsoft Access
您可以使用"导入"选项将存储在 Visual FoxPro 数据库中的数据导入到 Microsoft Access 数据库中。  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>将 Visual FoxPro 数据导入 Microsoft 访问数据库  
  
1.  打开 Microsoft 访问数据库。  
  
2.  从"文件"菜单中，选择"获取外部数据，然后导入"。  
  
3.  在"导入"对话框中，在"类型文件"列表中选择 ODBC 数据库。  
  
4.  在 SQL 数据源对话框中，选择连接到要查询的 FoxPro 数据的 Visual FoxPro 数据源，然后单击"确定"。  
  
5.  在"导入对象"对话框中，选择要导入的一个或多个表，然后单击"确定"。 您导入的 Visual FoxPro 表的名称将显示在 Microsoft Access 数据库的"表"选项卡中。  
  
 您现在可以使用 Microsoft Access 操作导入的 Visual FoxPro 表中的数据。 您导入的数据是存储在 Visual FoxPro 中的数据的快照;对导入的数据所做的更改不会发送回 Visual FoxPro 数据源。  
  
 如果您希望在 Microsoft Access 中进行更改以更改 Visual FoxPro 数据源上的数据，请参阅[从 Microsoft Access 查询和更新 Visual FoxPro 数据](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md)。
