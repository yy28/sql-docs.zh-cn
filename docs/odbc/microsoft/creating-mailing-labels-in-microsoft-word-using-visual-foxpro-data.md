---
title: 使用 Visual FoxPro 数据在 Microsoft Word 中创建邮件标签 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data [ODBC], mailing labels
- Visual FoxPro data [ODBC], Word
- mailing labels [ODBC]
- Visual FoxPro ODBC driver [ODBC], Word
- FoxPro ODBC driver [ODBC], word
ms.assetid: c901b60c-9f84-407a-b3d1-b4d301a71370
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73880171493555a7d30e5c0c5419d02338961e9b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096533"
---
# <a name="creating-mailing-labels-in-microsoft-word-using-visual-foxpro-data"></a>使用 Visual FoxPro 数据在 Microsoft Word 中创建邮件标签
可以在 Microsoft Word for Windows 95 或 Windows 98 文档中使用 Visual FoxPro 数据。 例如，你可能想要从存储在 Visual FoxPro 表中的客户信息创建邮件标签。  
  
### <a name="to-create-mailing-labels"></a>创建邮件标签  
  
1.  在 Microsoft Word 中创建一个新的空白文档。  
  
2.  从 "工具" 菜单中选择 "邮件合并"。  
  
3.  在邮件合并助手中，选择 "创建"，然后选择 "邮件标签"。  
  
4.  在 "主文档" 下，选择 "活动窗口"。  
  
5.  在 "数据源" 下，选择 "获取数据"，然后选择 "打开数据源"。  
  
6.  在 "打开数据源" 对话框中，选择 "MS Query"。  
  
7.  在 "选择数据源" 对话框中，选择一个 Visual FoxPro 数据源，然后单击 "使用"。  
  
8.  如果数据源访问的数据库包含表，请从 "添加表" 对话框中选择一个表。 Microsoft Query 显示查询设计器上半部分的已添加表。  
  
9. 通过从表中将字段拖到设计器的下半部分，为查询选择字段。  
  
10. 从 "文件" 菜单中选择 "将数据返回给 Microsoft Word"。 Microsoft Query 将关闭，你选择的数据可在邮件合并文档中使用。  
  
11. 在主文档下，选择 "设置"。  
  
12. 在 "标签选项" 对话框中，选择所需的打印机和标签信息，然后单击 "确定"。  
  
13. 在 "创建标签" 对话框中，选择要在邮件标签上打印的字段，然后单击 "确定"。  
  
14. 在邮件合并帮助器的 "将数据与文档合并" 下，单击 "合并"。  
  
15. 在 "合并" 对话框中，选择所需的选项，然后单击 "合并"。
