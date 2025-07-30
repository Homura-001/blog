# [SWPUCTF 2021 新生赛]gift_F12![image-20250729195849039](E:\note_ctf\assets\image-20250729195849039.png)

我还以为是要改今天的时间

# [SWPUCTF 2021 新生赛]jicao

![image-20250729200411948](E:\note_ctf\assets\image-20250729200411948.png)

要求post传入id值为wllNB，直接上传

## JSON

JSON（JavaScript Object Notation） 是一种轻量级的数据交换格式，它以易于阅读和编写的文本形式表示数据。JSON 最初是为JavaScript开发 的，但已成为一种 通用的数据格式，常用于数据存储与交换。

JSON 数据格式的特点

优势	具体描述
键值对结构	JSON 数据是以 键值对 的形式表示的，键值对的结构使得 JSON 非常适合表示结构化数据。
跨语言兼容性	JSON 是一种 独立于编程语言的数据格式，因此 可以在不同编程语言之间轻松传输和解析数据，几乎所有现代编程语言都支持 JSON 的编码和解码。
支持的数据类型	JSON 支持多种数据类型，包括 字符串、数字、布尔值、数组、null 以及 JSON。
不支持注释	JSON 主要用于对数据的描述，故 JSON 不支持注释，这意味着你 不能在 JSON 数据中添加注释以解释数据的含义。
无循环引用	JSON 不支持循环引用，也就是说，JSON 中的键值对不能引用包含它的对象，这有助于避免数据结构的无限递归。
支持嵌套	JSON 内部可以嵌套 JSON 数据。

```
{
  "name": "John",
  "age": 30,
  "hometown": "New York",
  "pets": [
    {
      "name": "Fido",
      "species": "dog"
    },
    {
      "name": "Fluffy",
      "species": "cat"
    }
  ],
  "car": null
}
```

> [!CAUTION]
>
> JSON 数据中，`键必须为字符串`，而值可以是 `字符串`、`数值`、`布尔值`、`数组`、`JSON` 或 `null`。
>
> JSON 格式中，字符串 `必须使用双引号而不能使用单引号`。

## json_decode() 

可以对JSON字符串解码，并转换为PHP变量

```
mixed json_decoce( $json_str, assoc, depth, options )
```

$json_str ：需要解码的JSON字符串，只能处理UTF-8编码的数据
assoc ：布尔类型，true返回数组，（默认）false返回对象
depth ：整数类型，递归的深度（默认512层），最大 2147483647 层
options ：二进制掩码，目前只支持 JSON_BIGINT_AS_STRING

<?php


# 定义 JSON 数据
```
$json_content = '{
    "name": "John",
    "age": 30,
    "hometown": "New York",
    "pets": [
        {
            "name": "Fido",
            "species": "dog"
        },
        {
            "name": "Fluffy",
            "species": "cat"
        }
    ],
    "car": null
}';

print('【将 JSON 数据解析为对象进行返回】' . "\n");
$result_1 = json_decode($json_content);
var_dump($result_1);

print("\n" . '【将 JSON 数据解析为关联数组进行返回' . "\n");
$result_2 = json_Decode($json_content, true);
var_dump($result_2);
```

```
【将 JSON 数据解析为对象进行返回】
object(stdClass)#1 (5) {
  ["name"]=>
  string(4) "John"
  ["age"]=>
  int(30)
  ["hometown"]=>
  string(8) "New York"
  ["pets"]=>
  array(2) {
    [0]=>
    object(stdClass)#2 (2) {
      ["name"]=>
      string(4) "Fido"
      ["species"]=>
      string(3) "dog"
    }
    [1]=>
    object(stdClass)#3 (2) {
      ["name"]=>
      string(6) "Fluffy"
      ["species"]=>
      string(3) "cat"
    }
  }
  ["car"]=>
  NULL
}

【将 JSON 数据解析为关联数组进行返回
array(5) {
  ["name"]=>
  string(4) "John"
  ["age"]=>
  int(30)
  ["hometown"]=>
  string(8) "New York"
  ["pets"]=>
  array(2) {
    [0]=>
    array(2) {
      ["name"]=>
      string(4) "Fido"
      ["species"]=>
      string(3) "dog"
    }
    [1]=>
    array(2) {
      ["name"]=>
      string(6) "Fluffy"
      ["species"]=>
      string(3) "cat"
    }
  }
  ["car"]=>
  NULL
}
```

## **var_dump()** 

用于输出变量的相关信息。

显示关于一个或多个表达式的结构信息，包括表达式的类型与值。数组将递归展开值，通过缩进显示其结构。

PHP 版本要求: PHP 4, PHP 5, PHP 7

```
<?php
$a = array(1, 2, array("a", "b", "c"));
var_dump($a);
?>
```

```
array(3) {
  [0]=>
  int(1)
  [1]=>
  int(2)
  [2]=>
  array(3) {
    [0]=>
    string(1) "a"
    [1]=>
    string(1) "b"
    [2]=>
    string(1) "c"
  }
}
```

