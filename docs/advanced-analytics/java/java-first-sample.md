---
title: Java 示例，并适用于 SQL Server 2019-SQL Server 机器学习服务教程
description: 若要了解有关使用 SQL Server 数据的 Java 语言扩展的步骤的 SQL Server 2019 上运行 Java 示例代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 000318716b07f58e94bd5c482d9c349e5d4e5481
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473761"
---
# <a name="sql-server-regex-java-sample"></a>SQL Server 正则表达式 Java 示例

此示例演示如何从 SQL Server 接收两个列 （ID 和文本），并还会将正则表达式作为输入参数的 Java 类。 类返回到 SQL Server （ID 和文本） 返回两个列。

对于给定的文本发送到的 Java 类的文本列中，代码会检查是否给定的正则表达式实现，并返回该文本与原始 id。 

此特定示例使用正则表达式，用于检查如果文本包含词"Java"或"java"。

## <a name="microsoft-extensibility-sdk-for-java-for-microsoft-sql-server"></a>Microsoft 扩展适用于 Microsoft SQL Server 的 Java SDK

 在 ctp 版本 2.5 中，我们正在更改实现用于 Java 语言扩展通信与 SQL Server 的 Java 代码的方式。 与通过 Java SQL Server 进行交互时，这将提供更好的开发人员体验。

为帮助器接口，这将使轻松实现对 SQL Server 运行的 Java 代码，应考虑 SDK。

> [!NOTE]
> SDK 的引入是从以前的 Ctp 一项重大更改。 您必须使用任何上一示例将需要更新，以使用 SDK。

有关详细信息，请参阅[SDK 文档](java-sdk.md)。

## <a name="prerequisites"></a>先决条件

+ SQL Server 2019 数据库引擎实例使用的可扩展性框架和 Java 编程扩展[在 Windows 上](../install/sql-machine-learning-services-windows-install.md)或[Linux 上](https://docs.microsoft.com/sql/linux/sql-server-linux-setup)。 系统配置的详细信息，请参阅[Java 语言扩展。 在 SQL Server 2019](extension-java.md)。 有关编码要求的详细信息，请参阅[如何在 SQL Server 中调用 Java](howto-call-java-from-sql.md)。

+ SQL Server Management Studio 或 Azure Data Studio 运行 T-SQL。

+ Java SE 开发工具包 (JDK) 8 或 JRE 8 上的 Windows 或 Linux。

+ [适用于 Microsoft SQL Server 的 Microsoft Java 扩展性 SDK](http://aka.ms/mssql-java-lang-extension) mssql java lang extension.jar。

使用命令行编译**javac**对于本教程来说已足够。

## <a name="1---create-sample-data-in-a-sql-server-table"></a>1-在 SQL Server 表中创建示例数据

首先，创建并填充*testdata*表与**ID**并**文本**列。 连接到 SQL Server 并运行以下脚本来创建表：

```sql
CREATE DATABASE javatest
GO
USE javatest
GO

-- Create table for test data
DROP TABLE IF exists testdata;
GO

CREATE TABLE testdata(
id int NOT NULL,
"text" nvarchar(100) NOT NULL)
GO

TRUNCATE TABLE testdata
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
Select * FROM testdata
```

## <a name="2---class-regexsamplejava"></a>2-类 RegexSample.java

首先创建主类。

在此步骤中，将创建一个名为类**RegexSample.java**并将以下 Java 代码复制到该文件。

此主类导入的 SDK，这意味着，在步骤 1 中下载的 jar 文件必须是可发现此类中。

> [!NOTE]
> 请注意此类导入 Java 扩展 SDK 包。
，请参阅文章[Microsoft 扩展性 SDK for Java 的 Microsoft SQL Server](java-sdk.md)的更多详细信息。

```java
package pkg;

import com.microsoft.sqlserver.javalangextension.PrimitiveDataset;
import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionExecutor;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.ListIterator;
import java.util.regex.*;

public class RegexSample extends AbstractSqlServerExtensionExecutor {
    private Pattern expr;

    public RegexSample() {
        // Setup the expected extension version, and class to use for input and output dataset
        executorExtensionVersion = SQLSERVER_JAVA_LANG_EXTENSION_V1;
        executorInputDatasetClassName = PrimitiveDataset.class.getName();
        executorOutputDatasetClassName = PrimitiveDataset.class.getName();
    }
    
    public PrimitiveDataset execute(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Validate the input parameters and input column schema
        validateInput(input, params);

        int[] inIds = input.getIntColumn(0);
        String[] inValues = input.getStringColumn(1);
        int rowCount = inValues.length;

        String regexExpr = (String)params.get("regexExpr");
        expr = Pattern.compile(regexExpr);

        System.out.println("regex expression: " + regexExpr);

        // Lists to store the output data
        LinkedList<Integer> outIds = new LinkedList<Integer>();
        LinkedList<String> outValues = new LinkedList<String>();

        // Evaluate each row
        for(int i = 0; i < rowCount; i++) {
            if (check(inValues[i])) {
                outIds.add(inIds[i]);
                outValues.add(inValues[i]);
            }
        }

        int outputRowCount = outValues.size();

        int[] idOutputCol = new int[outputRowCount];
        String[] valueOutputCol = new String[outputRowCount];

        // Convert the list of output columns to arrays
        outValues.toArray(valueOutputCol);

        ListIterator<Integer> it = outIds.listIterator(0);
        int rowId = 0;

        System.out.println("Output data:");
        while (it.hasNext()) {
            idOutputCol[rowId] = it.next().intValue();

            System.out.println("ID: " + idOutputCol[rowId] + " Value: " + valueOutputCol[rowId]);
            rowId++;
        }

        // Construct the output dataset
        PrimitiveDataset output = new PrimitiveDataset();

        output.addColumnMetadata(0, "ID", java.sql.Types.INTEGER, 0, 0);
        output.addColumnMetadata(1, "Text", java.sql.Types.NVARCHAR, 0, 0);

        output.addIntColumn(0, idOutputCol, null);
        output.addStringColumn(1, valueOutputCol);

        return output;
    }

    private void validateInput(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Check for the regex expression input parameter
        if (params.get("regexExpr") == null) {
            throw new IllegalArgumentException("Input parameter 'regexExpr' is not found");
        }

        // The expected input schema should be at least 2 columns, (INTEGER, STRING)
        if (input.getColumnCount() < 2) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }

        // Check that the input column types are expected
        if (input.getColumnType(0) != java.sql.Types.INTEGER &&
                (input.getColumnType(1) != java.sql.Types.VARCHAR && input.getColumnType(1) == java.sql.Types.NVARCHAR )) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }
    }

    private boolean check(String text) {
        Matcher m = expr.matcher(text);

        return m.find();
    }
}
```

## <a name="3-compile-and-create-jar-file"></a>3 编译并创建.jar 文件

我们建议您打包您的类和依赖项的.jar 文件。 当你生成/编译项目时，大多数的 Java Ide，如支持 Eclipse 或 IntelliJ 生成 jar 文件。 在此示例中，我们具有名为 jar 文件**regex.jar**。

如果要手动创建.jar 文件，可以按照的步骤，请参阅[如何创建一个 jar 文件](extension-java.md#create-jar)。

> [!NOTE]
> 此示例使用的包，这意味着包"pkg"在类的顶部提供可确保已编译的代码保存在名为"pkg"的子文件夹中。 这会自动处理的如果使用 IDE，但是，如果您正在进行手动编译使用的类**javac**，将需要手动将已编译的代码放在 pkg 子文件夹中。

## <a name="4---create-external-libraries"></a>4-创建外部库

通过创建外部库，SQL Server 将自动获取访问权限的 jar 文件并不需要设置为类路径中的任何特殊权限。

在此示例中，需要创建两个外部库。 对于 SDK，其中一个，另一个用于正则表达式 Java 示例。

1.  下载[Microsoft 扩展性 SDK for Java 的 Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension) mssql java lang extension.jar。

1. 创建外部库 sdk

```sql
-- Create external library for the SDK
CREATE EXTERNAL LIBRARY sdk
FROM (CONTENT = '<path>/mssql-java-lang-extension.jar')
WITH (LANGUAGE = 'Java');
GO
```

3. 创建外部库的正则表达式示例

```sql
-- Create external library for the regex sample
CREATE EXTERNAL LIBRARY regex
FROM (CONTENT = '<path>/regex.jar')
WITH (LANGUAGE = 'Java');
GO
```

## <a name="5---set-permissions-skip-if-you-performed-step-4"></a>5-设置权限 （跳过如果执行步骤 4）

如果您使用外部库，则无需此步骤。 工作的推荐的方法是从您的 jar 中创建的外部库。

如果不想要使用外部库，需要设置必要的权限。 如果进程标识有权访问你的代码，才会成功执行脚本。 您可以找到有关设置权限的详细信息[此处](extension-java.md)。

### <a name="on-linux"></a>Linux 上

授予读取/执行权限到 classpath **mssql_satellite**用户。

### <a name="on-windows"></a>在 Windows 上

将读取和执行权限授予**SQLRUserGroup**并**应用程序的所有包**上包含已编译的 Java 代码的文件夹的 SID。 

整个树必须具有的权限，从根父到最后一个子文件夹。 
 
1. 右键单击文件夹 (例如，C:\myJavaCode) 中，选择**属性** > **安全**。
2. 单击 **“编辑”**。
3. 单击 **“添加”**。
4. 在中**选择用户、 计算机、 服务帐户或组**:
   + 单击**对象类型**，并确保*内置的安全原则*并*组*选择。
   + 单击**位置**选择本地计算机名称列表的顶部。
5. 输入**SQLRUserGroup**，检查的名称，然后单击确定以添加组。
6. 输入**所有应用程序包**，请检查名称，并单击确定以添加。 如果名称不能解决，重新访问位置步骤。 SID 是计算机本地。

请确保这两个安全标识对文件夹和"pkg"子文件夹具有读取和执行权限。

<a name="call-method"></a>

## <a name="2---call-the-java-class"></a>2-调用的 Java 类

若要从 SQL Server 调用 Java 代码，我们将创建调用 sp_execute_external_script 的存储的过程。 在"脚本"参数中，我们将定义哪个 [包]。[类] 我们想要调用。 在此示例中，类属于名为的包**pkg**和一个类文件称为**RegexSample.java**。

> [!NOTE]
>我们不定义要调用的方法。 默认情况下**执行**将调用方法。 这意味着，你需要遵循的 SDK 接口并实现一个 execute 方法在 Java 类中，如果你想要能够从 SQL Server 调用类。

```sql
/*
This stored procedure takes an input query (input dataset) and a regular expression and returns the rows that fulfilled the given regular expression. This sample uses a regular expression that checks if a text contains the word "Java" or "java" ([Jj]ava) 
*/

CREATE OR ALTER PROCEDURE [dbo].[java_regex] @expr nvarchar(200), @query nvarchar(400)
AS
BEGIN
--Call the Java program by giving the package.className in @script
--The method invoked in the Java code is always the "execute" method
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.RegexSample'
, @input_data_1 = @query
, @params = N'@regexExpr nvarchar(200)'
, @regexExpr = @expr
with result sets ((ID int, text nvarchar(100)));
END
GO

--Now execute the above stored procedure and provide the regular expression and an input query
EXECUTE [dbo].[java_regex] N'[Jj]ava', N'SELECT id, text FROM testdata'
GO
```

### <a name="results"></a>结果

执行后调用，应获取的结果集包含两个行。

![Java 示例而得出](../media/java/java-sample-results.png "示例结果")

### <a name="if-you-get-an-error"></a>如果收到错误

+ 在编译您的类时，"pkg"子文件夹应包含所有三个类的已编译的代码。

+ 最后，如果不使用外部库，检查的权限*每个*文件夹中，从根到"pkg"子文件夹，以确保运行外部进程的安全标识有权读取和执行您的代码。

## <a name="next-steps"></a>后续步骤

+ [Microsoft 扩展适用于 Microsoft SQL Server 的 Java SDK](java-sdk.md)
+ [如何在 SQL Server 中调用 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 扩展](extension-java.md)
+ [Java 和 SQL Server 数据类型](java-sql-datatypes.md)
