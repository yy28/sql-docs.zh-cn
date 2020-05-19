---
title: 在对象资源管理器中查看空间数据
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 59cca562-e3f5-4257-b868-adcbcc0142cc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8e8b5a8765523c91c00aae362ae311deff3179eb
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718164"
---
# <a name="view-spatial-data-in-object-explorer"></a>在对象资源管理器中查看空间数据
  查询编辑器中的 **“空间结果”** 窗口中提供了一些可视化工具，可用来查看空间数据结果以及在 **“结果”** 窗口中以网格格式显示的数据。 若要在 **“空间结果”** 窗口中显示空间数据，则查询结果中必须至少包括一个包含几何图形或地域数据的空间数据列。  
  
### <a name="to-view-spatial-data-in-the-spatial-results-window"></a>在“空间结果”窗口中查看空间数据  
  
1.  在查询编辑器中单击 **“空间结果”** 选项卡。  
  
    > [!NOTE]  
    >  如果查询结果中不包含空间数据或者指定将结果作为文本返回，则此窗口不可用。  
  
2.  从 **“选择空间列”** 列表中选择要查看的列。 如果表中只有一个空间列，则此列是列表中的默认选项。  
  
3.  从“选择标签列”  列表中选择要用作数据标签的非空间列。  
  
4.  从 **“选择投影”** 列表中选择地域数据所需的投影。 默认投影为 Equirectangular；其他可用投影为 Mercator、Robinson 或 Bonne。  
  
    > [!NOTE]  
    >  如果空间列中包含几何图形数据，则“选择投影”  不可用。  
  
5.  调整 **“缩放”** 滑块可增加映射元素的可视大小。 对于多边形形状，仅当形状大到能够容纳标签文本时，标签才可见。  
  
## <a name="see-also"></a>另请参阅  
 [“空间结果”窗口](spatial-results-window.md)   
 [数据库引擎查询编辑器 (SQL Server Management Studio)](database-engine-query-editor-sql-server-management-studio.md)   
 [查询和文本编辑器 (SQL Server Management Studio)](query-and-text-editors-sql-server-management-studio.md)  
  
  
