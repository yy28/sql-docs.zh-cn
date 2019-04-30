---
title: ConvertToString 方法 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 426fd1fdcd3931981037b346b048de816e8596d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280878"
---
# <a name="converttostring-method-rds"></a>ConvertToString 方法 (RDS)
将转换[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)为 MIME 字符串，表示记录集数据。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataFactory*  
 表示的对象变量[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象。  
  
 *Recordset*  
 表示的对象变量**记录集**对象。  
  
## <a name="remarks"></a>备注  
 相应的.asp 文件后，使用**ConvertToString**嵌入**记录集**服务器传输到客户端计算机上生成的 HTML 页面中。  
  
 **ConvertToString**第一次加载**记录集**游标服务到表，并生成流 MIME 格式。  
  
 在客户端，远程数据服务可以将 MIME 字符串转换回完全正常运行**记录集**。 它非常适合处理少于 400 使用不超过 1024 个字节宽度每行的数据行。 不应将其用于流式处理 BLOB 数据，并通过 HTTP 对大型结果集。 极大型数据集将通过 HTTP 与网络优化 tablegram 格式定义和部署的远程数据服务作为其本机传输协议格式相比到传输需要相当长的时间字符串，对执行没有在线压缩。  
  
> [!NOTE]
>  如果您使用 Active Server Pages 的客户端 HTML 页中嵌入生成的 MIME 字符串，请注意，早于 2.0 版的 VBScript 版本字符串的大小限制为 32 K。 如果超出此限制，则返回错误。 使用 MIME 嵌入通过相应的.asp 文件时，请查询作用域相对较小。 若要解决此问题，请从 Microsoft Windows 脚本技术网站下载最新版本的 VBScript。  
  
## <a name="applies-to"></a>适用范围  
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>请参阅  
 [ConvertToString 方法示例 (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [ConvertToString 方法示例 (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


