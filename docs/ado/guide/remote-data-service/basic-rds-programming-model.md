---
title: "基本的 RDS 编程模型 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d99d092b91ed150a3ad9163f2c4f7e513554e9f4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="basic-rds-programming-model"></a>基本的 RDS 编程模型
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 处理在以下环境中存在的应用程序： 客户端应用程序指定将在一台服务器并返回所需的信息所需的参数执行程序。 在服务器提升访问到指定的数据源中，调用程序检索的信息、 （可选） 处理数据，然后返回到客户端应用程序可以轻松地使用窗体中的所生成的信息。 RDS 提供了一种为你执行以下操作序列：  
  
-   指定要在服务器上，调用的程序，并获取一种方法来从客户端引用它。 (有时称为此引用*代理*。 它表示远程服务器程序。 客户端应用程序将"调用"代理就像它是本地的程序，但实际上，它调用的远程服务器程序。）  
  
-   调用服务器程序。 将参数传递给服务器计划标识数据源，并且要发出的命令。 （服务器程序实际使用 ADO 来获得对数据源的访问。 ADO 使与给定的参数之一的连接，然后发出另一个参数中指定的命令。）  
  
-   服务器计划获取[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从数据源的对象。 （可选）**记录集**在服务器上处理对象。  
  
-   服务器程序将返回最后一个**记录集**到客户端应用程序对象。  
  
-   在客户端，**记录集**对象放到可以轻松地使用由 visual 控件的窗体。  
  
-   对进行任何修改**记录集**对象发送回服务器计划，使用它们来更新数据源。  
  
 此编程模型包含某些便利功能。 如果你不需要复杂的服务器程序访问数据源，并且 rds-如果你提供所需的连接和命令参数，将自动检索简单，默认的服务器程序与指定的数据。  
  
 如果你需要更复杂的处理，则可以指定你自己的自定义服务器程序。 例如，由于自定义服务器程序具有 ADO 所掌握的完整功能，它无法连接到多个不同的数据源、 某些复杂的方式，合并其数据，然后返回到客户端应用程序的简单、 处理结果中。  
  
 最后，如果你的需求是在此期间的某处，ADO 现在支持自定义默认服务器程序的行为。  
  
## <a name="see-also"></a>另请参阅  
 [在详细信息的 RDS 编程模型](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



