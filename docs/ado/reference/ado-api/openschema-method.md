---
title: "OpenSchema 方法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e5c547eb8a6c1208bedffb988096f45b4c871d09
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="openschema-method"></a>OpenSchema 方法
从提供程序获取数据库架构信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>返回值  
 返回[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)包含架构信息的对象。 **记录集**将作为只读的、 静态游标打开。 *QueryType*确定列显示在**记录集**。  
  
#### <a name="parameters"></a>Parameters  
 *QueryType*  
 任何[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)值，该值表示架构运行查询的类型。  
  
 *条件*  
 可选。 数组的每个查询约束*QueryType*选项，因为列入[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)。  
  
 *SchemaID*  
 提供程序架构查询未定义的 OLE DB 规范的 GUID。 此参数是必需的如果*QueryType*设置为**adSchemaProviderSpecific**; 否则为不使用它。  
  
## <a name="remarks"></a>注释  
 **OpenSchema**方法返回有关数据源，例如什么表是在数据源，在表中，列中的自我描述的信息和支持数据类型。  
  
 *QueryType*自变量是一个 GUID，指示返回的列 （架构）。 OLE DB 规范有架构的完整列表。  
  
 *条件*自变量将限制架构查询的结果。 *条件*指定必须出现的值的数组中的列，称为约束的列，在产生的相应子集**记录集**。  
  
 常量**adSchemaProviderSpecific**用于*QueryType*参数如果提供程序定义外部那些自己非标准架构查询前面列出。 当使用此常量时， *SchemaID*参数为所需将架构查询要执行的 GUID。 如果*QueryType*设置为**adSchemaProviderSpecific**但*SchemaID*未提供将产生一个错误。  
  
 提供程序不需要支持所有的 OLE DB 标准架构查询。 具体而言，仅**adSchemaTables**， **adSchemaColumns**，和**adSchemaProviderTypes**所需的 OLE DB 规范。 但是，该提供程序不需要支持*条件*约束前面列出的这些架构查询。  
  
> [!NOTE]
>  **远程数据服务使用情况** **OpenSchema**方法不是可在客户端上[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
> [!NOTE]
>  在 Visual Basic 中，列中具有的 4 字节无符号的整数 (DBTYPE UI4)**记录集**从返回**OpenSchema**方法**连接**对象不能与其他变量进行比较。 有关 OLE DB 数据类型的详细信息，请参阅[OLE DB (OLE DB) 中的数据类型](http://msdn.microsoft.com/en-us/6039292f-74e0-49b2-b133-17bc117ebf6a)和[附录 a： 数据类型](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6)Microsoft OLE DB 程序员参考中。  
  
> [!NOTE]
>  **Visual C/c + + 用户**不使用客户端游标时，检索 ADO 中的列架构"ORDINAL_POSITION"返回类型 VT_R8 MDAC 2.7、 MDAC 2.8 和 MDAC 中使用的类型时的 Windows 数据访问组件 (Windows DAC) 6.0 中的变体2.6 已 VT_I4。 编写为 MDAC 2.6 变体使仅查找的程序返回的类型 VT_I4 将获取每个序号如果未进行修改的 MDAC 2.7、 MDAC 2.8 和 Windows DAC 6.0 下运行的零。 因为 OLE DB 返回的数据类型是 DBTYPE_UI4，进行此更改和签名的 VT_I4 类型中没有足够的空间以包含所有可能的值而不可能发生截断发生，从而导致数据丢失。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [OpenSchema 方法示例 (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [OpenSchema 方法示例 （VC + +）](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Open 方法 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 （ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)

