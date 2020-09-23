---
title: 从类文件创建 Java jar 文件
description: 使用 SQL Server 语言扩展执行 Java 代码时，将类文件打包到 jar 文件中。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c324fca6893af35cafe6e9f65eccd0e8a0e478f9
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180277"
---
# <a name="create-a-java-jar-file-from-class-files"></a>从类文件创建 Java jar 文件
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

使用 [SQL Server 语言扩展](../language-extensions-overview.md)执行 Java 代码时，了解如何将类文件打包到 jar 文件中。 建议将文件打包。

## <a name="create-a-jar-file"></a>创建 jar 文件

若要从类文件创建 jar 文件，请导航到包含类文件的文件夹，然后运行以下命令：

```cmd
jar -cf <MyJar.jar> *.class
```

确保指向 `jar.exe` 的路径是系统路径变量的一部分。 或者，指定到 jar 的完整路径，此路径可以在 JDK 文件夹中的 `/bin` 下找到。 例如：

```cmd
C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class
```

## <a name="next-steps"></a>后续步骤

+ [如何在 SQL Server 语言扩展中调用 Java 运行时](../how-to/call-java-from-sql.md)