---
title: Java 示例，并适用于 SQL Server 2019-SQL Server 机器学习服务教程
description: 若要了解有关使用 SQL Server 数据的 Java 语言扩展的步骤的 SQL Server 2019 上运行 Java 示例代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/27/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 25deba880827cc7396082dac9a2c86cc4dd66cd8
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582570"
---
# <a name="sql-server-java-sample-walkthrough"></a>SQL Server Java 示例演练

此示例演示如何从 SQL Server 接收两个列 （ID 和文本），并返回到 SQL Server （ID 和 ngram） 返回两个列的 Java 类。 对于给定的 ID 和字符串组合，在代码中生成 ngrams （子字符串） 的排列返回这些排列以及原始 id。 Ngram 的长度由发送到 Java 类的参数定义。

## <a name="prerequisites"></a>先决条件

+ SQL Server 2019 数据库引擎实例使用的可扩展性框架和 Java 编程扩展[在 Windows 上](../install/sql-machine-learning-services-windows-install.md)或[Linux 上](https://docs.microsoft.com/sql/linux/sql-server-linux-setup)。 系统配置的详细信息，请参阅[Java 语言扩展。 在 SQL Server 2019](extension-java.md)。 有关编码要求的详细信息，请参阅[如何在 SQL Server 中调用 Java](howto-call-java-from-sql.md)。

+ SQL Server Management Studio 或另一个用于运行 T-SQL 的工具。

+ Java SE 开发工具包 (JDK) 8 在 Windows 或 Linux。

使用命令行编译**javac**对于本教程来说已足够。 

## <a name="1---load-sample-data"></a>1-加载示例数据

首先，创建并填充*评审*表与**ID**并**文本**列。 连接到 SQL Server 并运行以下脚本来创建表：

```sql
DROP TABLE IF exists reviews;
GO
CREATE TABLE reviews(
    id int NOT NULL,
    "text" nvarchar(30) NOT NULL)

INSERT INTO reviews(id, "text") VALUES (1, 'AAA BBB CCC DDD EEE FFF')
INSERT INTO reviews(id, "text") VALUES (2, 'GGG HHH III JJJ KKK LLL')
INSERT INTO reviews(id, "text") VALUES (3, 'MMM NNN OOO PPP QQQ RRR')
GO
```

## <a name="2---class-ngramjava"></a>2-类 Ngram.java

首先创建主类。 这是三个类的第一个。

在此步骤中，将创建一个名为类**Ngram.java**并将以下 Java 代码复制到该文件。 


```java
//We will package our classes in a package called pkg
//Packages are option in Java-SQL, but required for this sample.
package pkg;

import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Ngram {

    //Required: This is only required if you are passing data in @input_data_1
    //from SQL Server in sp_execute_external_script
    public static int[] inputDataCol1 = new int[1];
    public static String[] inputDataCol2 = new String[1];

    //Required: Input null map. Size just needs to be set to "1"
    public static boolean[][] inputNullMap = new boolean[1][1];

    //Required: Output data columns returned back to SQL Server
    public static int[] outputDataCol1;
    public static String[] outputDataCol2;

    //Required: Output null map. Is populated with true or false values 
    //to indicate nulls
    public static boolean[][] outputNullMap;

    //Optional: This is only required if parameters are passed with @params
    // from SQL Server in sp_execute_external_script
    // n is giving us the size of ngram substrings
    public static int param1;

    //Optional: The number of rows we will be returning
    public static int numberOfRows;

    //Required: Number of output columns returned
    public static short numberOfOutputCols;

    /*Java main method - Only for testing purposes outside of SQL Server
    public static void main(String... args) {
        //getNGrams();
    }*/

    //This is the method we will be calling from SQL Server
    public static void getNGrams() {

        System.out.println("inputDataCol1.length= "+ inputDataCol1.length);
        if (inputDataCol1.length == 0 ) {
            // TODO: Set empty return
            return;
        }
        //Using a stream to "loop" over the input data inputDataCol1.length. You can also use a for loop for this.
        final List<InputRow> inputDataSet = IntStream.range(0, inputDataCol1.length)
                .mapToObj(i -> new InputRow(inputDataCol1[i], inputDataCol2[i]))
                .collect(Collectors.toList());


        //Again, we are using a stream to loop over data
        final List<OutputRow> outputDataSet = inputDataSet.stream()
                // Generate ngrams of size n for each incoming string
                // Each invocation of ngrams returns a list. flatMap flattens
                // the resulting list-of-lists to a flat list.
                .flatMap(inputRow -> ngrams(param1, inputRow.text).stream().map(s -> new OutputRow(inputRow.id, s)))
                .collect(Collectors.toList());

        //Print the outputDataSet
        System.out.println(outputDataSet);

        //Set the number of rows and columns we will be returning
        numberOfOutputCols = 2;
        numberOfRows = outputDataSet.size();
        outputDataCol1 = new int[numberOfRows]; // ID column
        outputDataCol2 = new String[numberOfRows]; //The ngram column
        outputNullMap = new boolean[2][numberOfRows];// output null map

        //Since we don't have any null values, we will populate all values in the outputNullMap to false
        IntStream.range(0, numberOfRows).forEach(i -> {
            final OutputRow outputRow = outputDataSet.get(i);
            outputDataCol1[i] = outputRow.id;
            outputDataCol2[i] = outputRow.ngram;
            outputNullMap[0][i] = false;
            outputNullMap[1][i] = false;
        });
    }

    // Example: ngrams(3, "abcde") = ["abc", "bcd", "cde"].
    private static List<String> ngrams(int n, String text) {
        return IntStream.range(0, text.length() - n + 1)
                .mapToObj(i -> text.substring(i, i + n))
                .collect(Collectors.toList());
    }
}
```

## <a name="3---class-inputrowjava"></a>3 - Class InputRow.java

创建一个名为第二个类**InputRow.java**、 组成下面的代码，并保存到与相同的位置**Ngram.java**。

```java
package pkg;

//This object represents one input row
public class InputRow {
    public final int id;
    public final String text;

    public InputRow(final int id, final String text) {
        this.id = id;
        this.text = text;
    }
}
```

## <a name="4---class-outputrowjava"></a>4-类 OutputRow.java

第三个和最后一个类称为**OutputRow.java**。 复制代码并将另存为 OutputRow.java 中与其他相同的位置。

```java
package pkg;

//This object represents one output row
public class OutputRow {
    public final int id;
    public final String ngram;

    public OutputRow(final int id, final String ngram) {
        this.id = id;
        this.ngram = ngram;
    }

    @Override
    public String toString() { return id + ":" + ngram; }
}
```

## <a name="5---compile"></a>5-编译

一旦有您的类准备就绪后，运行 javac 将其编译为".class"文件 (`javac Ngram.java InputRow.java OutputRow.java`)。 应显示为本示例 （Ngram.class、 InputRow.class 和 OutputRow.class） 的三个.class 文件。

将已编译的代码放入子文件夹中的类路径位置称为"pkg"。 如果你正在开发工作站上，则此步骤，其中将文件复制到 SQL Server 计算机。

Classpath 是代码的已编译的位置。 例如，在 Linux 上，如果类路径是 / home/myclasspath /，然后.class 文件应在 / home/myclasspath/pkg。 步骤 7 中的示例脚本，在 sp_execute_external_script 中提供的类路径为 ' / home/myclasspath /' 中 （假设 Linux）。 

在 Windows 中，我们建议使用相对较浅表文件夹结构，一个或两个级别深度，以简化的权限。 例如，应用类路径可能如下所示 C:\myJavaCode 与名为 \pkg 包含已编译的类的子文件夹。 

有关类路径的详细信息，请参阅[设置 CLASSPATH](howto-call-java-from-sql.md#set-classpath)。 

### <a name="using-jar-files"></a>使用.jar 文件

如果你打算打包您的类和依赖项的.jar 文件，提供 sp_execute_external_script CLASSPATH 参数中的.jar 文件的完整路径。 例如，如果 jar 文件调用 ngram.jar，将为类路径 / home/myclasspath/ngram.jar Linux 上。

## <a name="6---create-external-library"></a>6-创建外部库

通过创建外部库，SQL Server 将自动获取访问权限，该 jar 文件并不需要设置为类路径中的任何特殊权限。

```sql 
CREATE EXTERNAL LIBRARY ngram
FROM (CONTENT = '<path>/ngram.jar') 
WITH (LANGUAGE = 'Java'); 
GO
```

## <a name="7---set-permissions-skip-if-you-performed-step-6"></a>7-设置权限 （跳过如果执行步骤 6）

如果您使用外部库，则无需此步骤。 工作的推荐的方法是从您的 jar 中创建的外部库。 

如果不想要使用外部库，需要设置必要的权限。 如果进程标识有权访问你的代码，才会成功执行脚本。 

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

## <a name="8---call-getngrams"></a>8 - Call *getNgrams()*

若要从 SQL Server 调用的代码，指定的 Java 方法**getNgrams()** sp_execute_external_script 的"脚本"参数中。 此方法属于名为"pkg"和一个名为的类文件的包**Ngram.java**。

此示例传递 CLASSPATH 参数来提供对 Java 文件路径。 它还使用"params"将参数传递给 Java 类。 请确保该 classpath 不超过 30 个字符。 如果是这样，增加以下脚本中的值。

+ 在 Linux 上，在 SQL Server Management Studio 或其他工具用于运行 TRANSACT-SQL 中运行下面的代码。 

+ 在 Windows 中，更改@myClassPathN'C:\myJavaCode 到\'（假设它 \pkg 的父文件夹） 中 SQL Server Management Studio 或其他工具执行查询前。

```sql
DECLARE @myClassPath nvarchar(50)
DECLARE @n int 
--This is where you store your classes or jars.
--This is the size of the ngram
SET @n = 3
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.Ngram.getNGrams'
, @input_data_1 = N'SELECT id, text FROM reviews'
, @parallel = 0
, @params = N'@param1 INT'
, @param1 = @n
with result sets ((ID int, ngram varchar(20)))
GO
```

### <a name="results"></a>结果

执行后调用，应会看到的结果集显示两个列：

![Java 示例而得出](../media/java/java-sample-results.png "示例结果")

### <a name="if-you-get-an-error"></a>如果收到错误

+ 在编译您的类时，"pkg"子文件夹应包含所有三个类的已编译的代码。

+ 类路径的长度不能超过声明的值 (`DECLARE @myClassPath nvarchar(50)`)。 如果是这样，路径截断至前 50 个字符，并且将不会加载已编译的代码。 可以执行`SELECT @myClassPath`检查的值。 如果是不够的 50 个字符的长度提高。 

+ 最后，检查权限*每个*文件夹中，从根到"pkg"子文件夹，以确保运行外部进程的安全标识有权读取和执行您的代码。

## <a name="see-also"></a>另请参阅

+ [如何在 SQL Server 中调用 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 扩展](extension-java.md)
+ [Java 和 SQL Server 数据类型](java-sql-datatypes.md)
