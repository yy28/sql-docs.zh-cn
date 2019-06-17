---
title: 第 1 步：设置 Visual Basic 项目 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b5f6379eb6cfc1d0f9020019d543cda180d9d88b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700609"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>第 1 步：设置 Visual Basic 项目
在此方案中，假定您已用于 Internet 发布在系统上安装 Microsoft Visual Basic 6.0、 ADO 2.5 或更高版本，以及 Microsoft OLE DB 访问接口。 将首先创建一个新项目，并将某些控件添加到项目中的默认窗体。  
  
### <a name="to-create-an-ado-project"></a>若要创建 ADO 项目：  
  
1.  在 Microsoft Visual Basic 中，创建一个新的标准 EXE 项目。  
  
2.  从项目菜单中，选择引用。  
  
3.  选择"Microsoft ActiveX 数据对象 2.5 库"，然后单击确定。  
  
### <a name="to-insert-controls-on-the-main-form"></a>若要插入的主窗体上的控件：  
  
1.  将 ListBox 控件添加到 Form1 中。 将其名称属性设置为**lstMain**。  
  
2.  将另一个列表框控件添加到 Form1 中。 将其名称属性设置为**lstDetails**。  
  
3.  将 TextBox 控件添加到 Form1 中。 将其名称属性设置为**txtDetails**。  
  
## <a name="see-also"></a>请参阅  
 [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步骤 2：初始化主列表框](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
