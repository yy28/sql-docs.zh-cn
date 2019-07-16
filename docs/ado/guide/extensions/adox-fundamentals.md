---
title: ADOX 基础知识 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66965b99d0f8bcc87025239f7ffa54814e6d74f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923263"
---
# <a name="adox-fundamentals"></a>ADOX 基础知识
数据定义语言和安全 (ADOX) 的 Microsoft® ActiveX® 数据对象扩展是 ADO 对象和编程模型的扩展。 ADOX 包括架构创建和修改，以及安全的对象。 因为它是基于对象的架构操作方法，您可以编写代码来处理各种数据源而不考虑其本机语法之间的差异。  
  
 ADOX 是伴随库到核心 ADO 对象。 它公开用于创建、 修改和删除架构对象，如表和过程的其他对象。 它还包括安全对象来维护用户和组，并以授予和撤消对对象的权限。  
  
 若要使用你的开发工具 ADOX，应建立对 ADOX 类型库的引用。 ADOX 库的描述是"Microsoft ADO ext.DDL 和安全"。 ADOX 库文件名称为 Msadox.dll，，程序 ID (ProgID) 为"ADOX"。 有关建立对库的引用的详细信息，请参阅你的开发工具的文档。  
  
 Microsoft OLE DB Provider for Microsoft Jet 数据库引擎完全支持 ADOX。 可能不支持数据访问接口根据 ADOX 的某些功能。  
  
 本文档假定 Microsoft® Visual Basic® 编程语言和 ADO 的常规知识的知识。 ADO 的详细信息，请参阅[ADO 程序员指南](../../../ado/guide/ado-programmer-s-guide.md)。 ADOX 有关的详细概述信息，请参阅以下主题：  
  
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
