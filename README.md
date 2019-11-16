# Regular-expression

靶场测试环境-正则表达式测试


 <?php  
$key='flag{********************************}'; 
$Regular= preg_match("/zkaq.*key.{2,9}:\/.*\/(key*key)/i", trim($_GET["id"]), $match); 
if( $Regular ){  
  die('key: '.$key); 
}  


函数部分：

preg_match(正则表达式，匹配的字符串)
匹配第一个匹配正则的子字符串，未找到返回0，找到返回1

trim($_GET["id"]) 接受ID传参过来的字符串
trim函数（string,charlist） 
      string 必须   
      charlist 可选 如果省略，则移除下列所有字符 
            "\0" null
            "\t" 制符表
            "\n" 换行
            "\r" 回车
            ""  空格

if( $Regular ){  die('key: '.$key); }

if (1){}执行；if(0){}不执行；

die();输出，并退出。



正则表达式部分:

PHP的正则表达式要写在/ /之间。

.  匹配除换行符 \n 之外的任何单字符。

*   匹配前面的子表达式零次或多次。

{n,m}： m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。例如，"o{1,3}" 将匹配 "fooood" 中的前三个o。请注意在逗号和两个数之间不能有空格。

\： 将下一个字符标记为或特殊字符、或原义字符、或向后引用、或八进制转义符。例如， 'n' 匹配字符 'n'。'\n' 匹配换行符。序列 '\\' 匹配 "\"，而 '\(' 则匹配 "("。

i：标记指定不区分大小写。

：连接字符，直接输出。




"/zkaq.*key.{2,9}:\/.*\/(key*key)/i"


需要将其拆分成几部分：

1.  /zkaq.*/
2.  /key.{2,9}/
3.  / :\/.*\/ /
4.  / （key*key）/i

1.  /zkaq.*/
 表示开头为zkaq后面随意接除换行符 \n 之外的任何单字符，因为是.* 如果是*的话只能接zkaqqqq或者zkaq等
 直接输出zkaq
 
2.  /key.{2,9}/
表示key 后面随意接2-9个除换行符 \n 之外的任何单字符
keytouma

3. / :\/.*\/ /
  ：为连接字符可以直接输出，\为转义字符 转义后面的/ .*可以随意输出除换行符 \n 之外的任何单字符。
  后面的\/一样是转义字符，中间字符可以省略不管，直接输出:// （:/123/也可以）
  
4. / （key*key）/i
    key*key 中间可以插入 随意个数的y  keyyyyyykey 或者keykey 所以这里可其实是 y*key
    表示”ke”和”key”之间有0-N个字符”y”（N为非负整数）。
    输出keyyykey
  
key： zkaqkeytouma://keyyykey


最后在靶机上面?id=输入key

得到FLAG()：

key: flag{regular_god_code}












