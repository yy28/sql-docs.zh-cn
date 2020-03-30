---
title: 保存关系图上的所选的表
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- saving tables
ms.assetid: 86943b49-48f3-432c-8021-928c13edfbcf
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 9a5e54642e5ee6250d8c01294f7f618288236cc3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75255083"
---
# <a name="save-selected-tables-on-a-diagram-visual-database-tools"></a>保存关系图中所选的表 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果不希望保存在数据库关系图中所做的全部更改，则可以保存特定表或一组表。  
  
### <a name="to-save-selected-tables"></a>保存所选的表  
  
1.  在数据库关系图中，选择要保存的表。  
  
2.  在“文件”  菜单中，选择“保存选择”  。  
  
3.  保存所做的选择时，“保存”  对话框将显示数据库中会被更新的表列表。  
  
    如果希望在继续操作前将表列表以文本文件形式保存到项目目录中，请选择“保存文本文件”  。  
  
4.  在“保存”  对话框中，确认表列表，再选择“是”  保存这些表。  
  
    > [!NOTE]  
    > 表的列表除了包含所选的表之外，可能还包含其他表。 例如，如果更改了某列的数据类型，而该列参与了与另一个表的关系，那么这两个表都将包括在此列表中。  
  
## <a name="see-also"></a>另请参阅  
[处理数据库关系图](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
