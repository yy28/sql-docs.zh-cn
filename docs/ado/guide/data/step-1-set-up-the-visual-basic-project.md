---
title: "步骤 1： 设置 Visual Basic 项目 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8bfdee45f81b2b69e0d495b643878f599345edf5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="step-1-set-up-the-visual-basic-project"></a>步骤 1： 设置 Visual Basic 项目
在此方案中，假定您已用于 Internet 发布在系统上安装 Microsoft Visual Basic 6.0、 ADO 2.5 或更高版本，以及 Microsoft OLE DB 提供程序。 将首先创建一个新的项目，并将某些控件添加到项目中的默认窗体。  
  
### <a name="to-create-an-ado-project"></a>若要创建的 ADO 项目：  
  
1.  在 Microsoft Visual Basic 中，创建新的标准 EXE 项目。  
  
2.  从项目菜单中，选择引用。  
  
3.  选择"Microsoft ActiveX 数据对象 2.5 库"，然后单击确定。  
  
### <a name="to-insert-controls-on-the-main-form"></a>若要插入主窗体上的控件：  
  
1.  将一个列表框控件添加到 Form1。 将其名称属性设置为**lstMain**。  
  
2.  将另一个列表框控件添加到 Form1。 将其名称属性设置为**lstDetails**。  
  
3.  将文本框控件添加到 Form1。 将其名称属性设置为**txtDetails**。  
  
## <a name="see-also"></a>另请参阅  
 [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步骤 2：初始化主列表框](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
