---
title: 稀疏列 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7d4237e0-818f-4639-9093-d5ac9683fc71
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b65250d6bd0ea911ee0d043e2768ae04ce9264d4
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278689"
---
# <a name="sparse-columns"></a>稀疏列
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  稀疏列是对 Null 值采用优化的存储方式的普通列。 稀疏列减少了 Null 值的空间需求，但代价是检索非 Null 值的开销增加。 当至少能够节省 20% 到 40% 的空间时，才应考虑使用稀疏列。  
  
 当连接到 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]（或更高版本）的服务器时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC Driver 3.0 支持稀疏列。 可以使用 [SQLServerDatabaseMetaData.getColumns](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)、[SQLServerDatabaseMetaData.getFunctionColumns](../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md) 或 [SQLServerDatabaseMetaData.getProcedureColumns](../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md) 确定哪个列是稀疏列以及哪个列是列集列。  
  
 列集是返回非类型化 XML 形式的所有稀疏列的计算列。 当表中有很多列、大于 1024 或分别对这些稀疏列进行操作很烦琐时，应考虑使用列集。 列集最多可以包含 30,000 个列。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 此示例说明如何检测列集。 它还显示如何分析列集的 XML 输出，以便从稀疏列获取数据。  
  
 所列的第一个代码部分是您应该对服务器运行的 Transact-SQL。  
  
 所列的第二个代码部分是 Java 源代码。 编译应用程序之前，请更改连接字符串。  
  
### <a name="code"></a>代码  
  
```sql
use AdventureWorks  
CREATE TABLE ColdCalling  
(  
ID int IDENTITY(1,1) PRIMARY KEY,  
[Date] date,  
[Time] time,  
PositiveFirstName nvarchar(50) SPARSE,  
PositiveLastName nvarchar(50) SPARSE,  
SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
);  
GO  
  
INSERT ColdCalling ([Date], [Time])  
VALUES ('10-13-09','07:05:24')  
GO  
  
INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  
VALUES ('07-20-09','05:00:24', 'AA', 'B')  
GO  
  
INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  
VALUES ('07-20-09','05:15:00', 'CC', 'DD')  
GO  
```  
  
### <a name="code"></a>代码  
  
```java
import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;

import org.xml.sax.InputSource;

import java.io.StringReader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.Statement;

import org.w3c.dom.Document;
import org.w3c.dom.Node;
import org.w3c.dom.NodeList;

public class SparseColumns {
    public static void main(String args[]) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        ResultSet rs = null;

        try (Connection conn = DriverManager.getConnection(connectionUrl);
                Statement stmt = conn.createStatement();) {

            // Determine the column set column
            String columnSetColName = null;
            String strCmd = "SELECT name FROM sys.columns WHERE object_id=(SELECT OBJECT_ID('ColdCalling')) AND is_column_set = 1";
            rs = stmt.executeQuery(strCmd);

            if (rs.next()) {
                columnSetColName = rs.getString(1);
                System.out.println(columnSetColName + " is the set column!");
            }

            strCmd = "SELECT * FROM ColdCalling";
            rs = stmt.executeQuery(strCmd);

            // Iterate through the result set
            ResultSetMetaData rsmd = rs.getMetaData();

            DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
            DocumentBuilder db = dbf.newDocumentBuilder();
            InputSource is = new InputSource();
            while (rs.next()) {
                // Iterate through the columns
                for (int i = 1; i <= rsmd.getColumnCount(); ++i) {
                    String name = rsmd.getColumnName(i);
                    String value = rs.getString(i);

                    // If this is the column set column
                    if (name.equalsIgnoreCase(columnSetColName)) {
                        System.out.println(name);

                        // Instead of printing the raw XML, parse it
                        if (value != null) {
                            // Add artificial root node "sparse" to ensure XML is well formed
                            String xml = "<sparse>" + value + "</sparse>";

                            is.setCharacterStream(new StringReader(xml));
                            Document doc = db.parse(is);

                            // Extract the NodeList from the artificial root node that was added
                            NodeList list = doc.getChildNodes();
                            // This is the <sparse> node
                            Node root = list.item(0);
                            // These are the xml column nodes
                            NodeList sparseColumnList = root.getChildNodes();

                            // Iterate through the XML document
                            for (int n = 0; n < sparseColumnList.getLength(); ++n) {
                                Node sparseColumnNode = sparseColumnList.item(n);
                                String columnName = sparseColumnNode.getNodeName();
                                // Note that the column value is not in the sparseColumNode, it is the value of the first child of it
                                Node sparseColumnValueNode = sparseColumnNode.getFirstChild();
                                String columnValue = sparseColumnValueNode.getNodeValue();

                                System.out.println("\t" + columnName + "\t: " + columnValue);
                            }
                        }
                    }
                    else {   // Just print the name + value of non-sparse columns
                        System.out.println(name + "\t: " + value);
                    }
                }
                System.out.println();// New line between rows
            }
        }
        // Handle any errors that may have occurred.
        catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```  
  
## <a name="see-also"></a>另请参阅  
 [借助 JDBC 驱动程序提高性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
