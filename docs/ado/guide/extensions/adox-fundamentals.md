---
title: ADOX 基础知识 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX, fundamentals
ms.assetid: 954476fc-5f72-4ada-ace5-d9acb27d18f8
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8807daf163515780aa7f514a6145c4035ed3afc6
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273426"
---
# <a name="adox-fundamentals"></a>ADOX 基础知识
适用于数据定义语言和安全 (ADOX) 的 Microsoft® ActiveX® 数据对象扩展是对 ADO 对象和编程模型的扩展。 ADOX 包括架构创建和修改，以及安全的对象。 因为它是架构操作的基于对象的方法，你可以编写代码来处理各种数据源而不考虑其本机语法方面的差异。  
  
 ADOX 是对核心 ADO 对象的助理库。 它公开用于创建、 修改和删除架构对象，如表和过程的其他对象。 它还包括安全对象维护用户和组并将 grant 和 revoke 对象权限。  
  
 若要使用你的开发工具 ADOX，应建立对 ADOX 类型库的引用。 ADOX 库的说明为"Microsoft ADO 分机 DDL 和安全"。 ADOX 库文件名称即 Msadox.dll，并且程序 ID (ProgID) 是"ADOX"。 有关建立对库的引用的详细信息，请参阅你的开发工具的文档。  
  
 Microsoft OLE DB Provider for Microsoft Jet 数据库引擎完全支持 ADOX。 ADOX 的某些功能可能不被支持，具体取决于数据提供程序。  
  
 本文档假定的 Microsoft® Visual Basic 编程语言和 ADO 的常规知识的知识。 有关 ADO 的详细信息，请参阅[ADO 程序员指南](../../../ado/guide/ado-programmer-s-guide.md)。 有关 ADOX 的详细概述信息，请参阅以下主题：  
  
-   [ADOX 对象模型](../../../ado/reference/adox-api/adox-object-model.md)  
  
-   [ADOX 对象](../../../ado/reference/adox-api/adox-objects.md)  
  
-   [ADOX 集合](../../../ado/reference/adox-api/adox-collections.md)  
  
-   [ADOX 属性](../../../ado/reference/adox-api/adox-properties.md)  
  
-   [ADOX 方法](../../../ado/reference/adox-api/adox-methods.md)  
  
-   [ADOX 示例](../../../ado/reference/adox-api/adox-code-examples.md)  
  
## <a name="see-also"></a>请参阅  
 [ADOX API 参考](../../../ado/reference/adox-api/adox-api-reference.md)   
 [ADOX 代码示例](../../../ado/reference/adox-api/adox-code-examples.md)   
 [ADOX 集合](../../../ado/reference/adox-api/adox-collections.md)   
 [ADOX 枚举常量](../../../ado/reference/adox-api/adox-enumerated-constants.md)   
 [ADOX 方法](../../../ado/reference/adox-api/adox-methods.md)   
 [ADOX 对象模型](../../../ado/reference/adox-api/adox-object-model.md)   
 [ADOX 对象](../../../ado/reference/adox-api/adox-objects.md)   
 [ADOX 属性](../../../ado/reference/adox-api/adox-properties.md)   
 [ADO （多维） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [ADO 程序员指南](../../../ado/guide/ado-programmer-s-guide.md)
