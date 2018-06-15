---
title: ConvertToString 方法 (RDS) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 495ff412b2865cfbda4576f3b4631b850e2d37e3
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35287576"
---
# <a name="converttostring-method-rds"></a>ConvertToString 方法 (RDS)
将转换[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)表示的记录集数据的 MIME 字符串。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataFactory*  
 表示的对象变量[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象。  
  
 *Recordset*  
 表示的对象变量**记录集**对象。  
  
## <a name="remarks"></a>Remarks  
 发送相应的.asp 文件后，使用**ConvertToString**嵌入**记录集**以其传输到客户端计算机在服务器上生成的 HTML 页中。  
  
 **ConvertToString**首次加载**记录集**游标服务到表，，然后生成 MIME 格式的流。  
  
 客户端上远程数据服务可以将 MIME 字符串转换回完全正常运行**记录集**。 它适用于处理的数据与不能超过 1024 个字节宽度每行少于 400 行。 不应将其用于流式处理 BLOB 数据，并通过 HTTP 对大型结果集。 非常大型数据集将通过 HTTP 与网络优化的表图格式定义和部署的远程数据服务作为其自己的传输协议格式相比传输到需要相当长的时间对字符串中，不执行任何在线压缩。  
  
> [!NOTE]
>  如果使用 Active Server Pages 将生成的 MIME 字符串嵌入一个客户端的 HTML 页面，请注意，早于 2.0 版的 VBScript 版本限制为不超过 32k 的字符串的大小。 如果超出此限制，则返回错误。 使用 MIME 通过发送相应的.asp 文件嵌入时保持查询范围相对较小。 若要解决此问题，请从 Microsoft Windows 脚本技术网站下载最新版本的 VBScript。  
  
## <a name="applies-to"></a>适用范围  
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>请参阅  
 [ConvertToString 方法示例 (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [ConvertToString 方法示例 (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


