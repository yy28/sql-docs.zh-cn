---
title: ADOX 基础 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX, fundamentals
ms.assetid: 954476fc-5f72-4ada-ace5-d9acb27d18f8
author: rothja
ms.author: jroth
ms.openlocfilehash: 131df9d5712bf89c28e1b8e7eae30217b6c16947
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748179"
---
# <a name="adox-fundamentals"></a>ADOX 基础知识
Microsoft®用于数据定义语言和安全（ADOX）的 ActiveX®数据对象扩展是对 ADO 对象和编程模型的扩展。 ADOX 包含用于创建和修改架构以及安全性的对象。 由于它是一种基于对象的架构处理方法，因此你可以编写代码来处理各种数据源，而不考虑它们的本机语法差异。  
  
 ADOX 是核心 ADO 对象的配套库。 它公开了用于创建、修改和删除架构对象（如表和过程）的其他对象。 它还包括安全对象以维护用户和组以及授予和撤消对对象的权限。  
  
 若要在开发工具中使用 ADOX，应建立对 ADOX 类型库的引用。 ADOX 库的说明是 "Microsoft ADO Ext. DDL and Security"。 ADOX 库文件名为 Msadox，程序 ID （ProgID）为 "ADOX"。 有关建立对库的引用的详细信息，请参阅开发工具的文档。  
  
 Microsoft Jet 数据库引擎的 Microsoft OLE DB 提供程序完全支持 ADOX。 可能无法支持 ADOX 的某些功能，具体取决于您的数据访问接口。  
  
 本文档假定你了解 Microsoft® Visual Basic®编程语言和 ADO 的一般知识。 有关 ADO 的详细信息，请参阅[Ado 程序员指南](../../../ado/guide/ado-programmer-s-guide.md)。 有关 ADOX 的更多概述信息，请参阅以下主题：  
  
-   [ADOX 对象模型](../../../ado/reference/adox-api/adox-object-model.md)  
  
-   [ADOX 对象](../../../ado/reference/adox-api/adox-objects.md)  
  
-   [ADOX 集合](../../../ado/reference/adox-api/adox-collections.md)  
  
-   [ADOX 属性](../../../ado/reference/adox-api/adox-properties.md)  
  
-   [ADOX 方法](../../../ado/reference/adox-api/adox-methods.md)  
  
-   [ADOX 示例](../../../ado/reference/adox-api/adox-code-examples.md)  
  
## <a name="see-also"></a>另请参阅  
 [ADOX API 参考](../../../ado/reference/adox-api/adox-api-reference.md)   
 [ADOX 代码示例](../../../ado/reference/adox-api/adox-code-examples.md)   
 [ADOX 集合](../../../ado/reference/adox-api/adox-collections.md)   
 [ADOX 枚举常量](../../../ado/reference/adox-api/adox-enumerated-constants.md)   
 [ADOX 方法](../../../ado/reference/adox-api/adox-methods.md)   
 [ADOX 对象模型](../../../ado/reference/adox-api/adox-object-model.md)   
 [ADOX 对象](../../../ado/reference/adox-api/adox-objects.md)   
 [ADOX 属性](../../../ado/reference/adox-api/adox-properties.md)   
 [ADO （多维）（ADO MD）](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [ADO 程序员指南](../../../ado/guide/ado-programmer-s-guide.md)
