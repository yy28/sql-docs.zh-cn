---
title: OpenSchema 方法 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 32f8c0086f1f81103156e5f592bcd63b0a43dd73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66707104"
---
# <a name="openschema-method"></a>OpenSchema 方法
从提供程序获取数据库架构信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>返回值  
 返回[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，其中包含架构信息。 **记录集**将作为只读、 静态游标打开。 *QueryType*确定列显示在**记录集**。  
  
#### <a name="parameters"></a>Parameters  
 *QueryType*  
 任何[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)值，该值表示运行架构查询的类型。  
  
 *条件*  
 可选。 每个查询约束的数组*QueryType*选项，如下所示[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)。  
  
 *SchemaID*  
 未定义的 OLE DB 规范的提供程序架构查询的 GUID。 此参数是必需的如果*QueryType*设置为**adSchemaProviderSpecific**; 否则为不使用它。  
  
## <a name="remarks"></a>备注  
 **OpenSchema**方法将返回有关数据源，如在数据源中，列在表中，有的表的自描述信息和支持的数据类型。  
  
 *QueryType*参数是一个 GUID，指示返回的列 （架构）。 OLE DB 规范具有架构的完整列表。  
  
 *条件*参数将限制为架构查询的结果。 *条件*指定必须出现的值的数组中的列，称为约束的列，在生成的相应子集**记录集**。  
  
 常量**adSchemaProviderSpecific**用于*QueryType*参数如果访问接口定义外部那些其自己使用了非标准架构查询前面列出。 使用此常量时， *SchemaID*架构查询执行的 GUID 传递所需的参数。 如果*QueryType*设置为**adSchemaProviderSpecific**但*SchemaID*未提供会导致错误。  
  
 提供程序不需要支持所有 OLE DB standard 架构查询。 具体而言，仅**adSchemaTables**， **adSchemaColumns**，并**adSchemaProviderTypes**所需的 OLE DB 规范。 但是，该提供程序不需要支持*条件*约束前面列出的那些架构查询。  
  
> [!NOTE]
>  **远程数据服务使用情况** **OpenSchema**方法不是客户端上可用[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
> [!NOTE]
>  在 Visual Basic 中，具有四个字节无符号的整数 (DBTYPE UI4) 中的列**记录集**返回从**OpenSchema**方法**连接**对象不能与其他变量进行比较。 有关 OLE DB 数据类型的详细信息，请参阅[OLE DB (OLE DB) 中的数据类型](https://msdn.microsoft.com/6039292f-74e0-49b2-b133-17bc117ebf6a)和[附录 a:数据类型](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6)中的 Microsoft OLE DB 程序员参考。  
  
> [!NOTE]
>  **Visual C /C++用户**不使用客户端游标时，检索的列架构在 ADO 中的"ORDINAL_POSITION"返回类型 VT_R8 MDAC 2.7、 MDAC 2.8 和时所使用的类型的 Windows 数据访问组件 (Windows DAC) 6.0 中的变体在安装 MDAC 2.6 中，为 VT_I4。 为安装 MDAC 2.6 编写查找一个变体的唯一程序返回的类型 VT_I4 会得到每个序号 MDAC 2.7、 MDAC 2.8 和 Windows DAC 6.0 无需修改即可运行时才为零。 因为 OLE DB 返回数据类型为 DBTYPE_UI4，进行此更改和已签名的 VT_I4 类型中没有足够的空间以包含所有可能的值，而无需可能截断发生，从而导致数据丢失。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [OpenSchema 方法示例 (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [OpenSchema 方法示例 （VC + +）](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Open 方法 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
