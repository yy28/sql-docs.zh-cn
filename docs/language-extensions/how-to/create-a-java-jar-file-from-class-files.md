---
title: 从类文件创建 Java jar 文件
description: 了解如何从类文件创建 Java jar 文件
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e5a53eb4b8da04a799461dcb1e0cb32feff2fe6f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "73658859"
---
# <a name="create-a-java-jar-file-from-class-files"></a>从类文件创建 Java jar 文件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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