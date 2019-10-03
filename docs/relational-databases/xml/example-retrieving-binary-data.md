---
title: 例如：检索二进制数据 | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: c168c76d33ac90bc658fad86404aea45b322d037
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199468"
---
# <a name="example-retrieving-binary-data"></a>例如：检索二进制数据

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

下面的查询返回在 **varbinary(max)** 类型列中存储的产品照片。 在此查询中指定了 `BINARY BASE64` 选项，以便以 base64 编码格式返回二进制数据。

## <a name="example"></a>示例

```sql
USE AdventureWorks2012;
GO
SELECT ProductPhotoID, ThumbNailPhoto
FROM Production.ProductPhoto
WHERE ProductPhotoID=1
FOR XML RAW, BINARY BASE64 ;
GO
```

预期的结果如下：

```console
<row ProductModelID="1" ThumbNailPhoto="base64 encoded binary data"/>
```

## <a name="see-also"></a>另请参阅

[将 RAW 模式与 FOR XML 一起使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)
