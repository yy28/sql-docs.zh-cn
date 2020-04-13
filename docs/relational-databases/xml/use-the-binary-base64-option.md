---
title: 使用 BINARY BASE64 选项 | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: RothJa
ms.author: jroth
ms.openlocfilehash: 42b2e41bedbce625d38b9d73a06b62817419c92c
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665245"
---
# <a name="use-the-binary-base64-option"></a>使用 BINARY BASE64 选项

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

如果查询中指定了 BINARY BASE64 选项，则以 base64 编码格式返回二进制数据。

如果未在查询中指定 BINARY BASE64 选项，则默认情况下，AUTO 模式支持二进制数据的 URL 编码。 系统返回对数据库虚拟根的相对 URL 的引用。 此引用是对在其中执行查询的数据库的引用。 返回的引用可用于在后续操作中访问实际的二进制数据。 可通过 SQLXML ISAPI dbobject 查询实现此访问。 查询必须提供足够的信息用于识别图像。 此类信息可能包括主键的列。

## <a name="column-alias"></a>列别名

查询视图并使用 FOR XML AUTO 模式时，请不要为二进制列使用别名。 如果使用别名，则别名在二进制数据的 URL 编码中返回。 在后续操作中，别名没有意义。 无意义的别名和 URL 编码不能用于检索图像。

### <a name="cast-to-a-blob"></a>强制转换为 BLOB

在 SELECT 查询中，将任何列强制转换为二进制大型对象 (BLOB) 都会使该列成为临时实体。 作为临时实体，BLOB 会失去其关联的表名和列名。 此强制转换会导致 AUTO 模式查询生成错误，因为系统不知道将此值放在 XML 层次结构中的何处。

例如，请考虑下表及其一行。

```sql
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)
INSERT INTO MyTable VALUES (1, 0x7);
```

以下查询会生成错误，该错误由强制转换为二进制大型对象 (BLOB) 引起：

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO;
```

解决方案是将 BINARY BASE64 选项添加到 FOR XML 子句中。 如果删除强制转换，查询会生成正确结果。

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO, BINARY BASE64;
```

预期的正确结果如下：

```console
<MyTable Col1="1" Col2="Bw==" />
```

## <a name="see-also"></a>另请参阅

[将 AUTO 模式与 FOR XML 一起使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)
