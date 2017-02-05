---
layout: post
title: "普林斯顿大学算法课程 In.class学习笔记"
date: 2017-02-04 17:10:03 +0800
categories: Java
tag: algorithm
---
* content
{:toc}

在学校使用 __Java__ 进行文件读写时总是觉得很复杂，没有搞懂读写的来龙去脉,对于 [__Scanner__ ](http://docs.oracle.com/javase/7/docs/api/java/util/Scanner.html)类的使用方法也是不够清楚，每次都是要用才去查表。在 [__cousera__](https://www.coursera.org/learn/algorithms-part2) 上学习时，发现他的[ __In__](http://algs4.cs.princeton.edu/code/edu/princeton/cs/algs4/In.java.html) 类使用很方便，简单，只需要一个文件名就能够实现文件读。

__In__ 主体是使用 __Scanner__ 对文件进行读写， 而 __Scanner__ 是通过 __InputStream__ 实例化。本文从两个部分开始介绍 ： __Scanner__ 使用， __In__ 的使用。

## Scanner使用

__Scanner__ 是拆散输入流成为一个一个的短语。

### __Scanner__ 的构造函数

```java
1.Scanner(InputStream source)
2.Scanner(File source)
3.Scanner(File source, String charsetName)
4.Scanner(Path source)
5.Scanner(Path source, String charsetName)
6.Scanner(Readable source)
7.Scanner(ReadableByteChannel source)
8.Scanner(ReadableByteChannel source, String charsetName)
9.Scanner(String source)
```

因为只学通过输入流来构建的，所以只介绍第1种。

首先通过文件名称实例化一 __File__ 对象，再实例化一个输入流， __Scanner__ 对象再操作输入流；

```java
try {
  //输入一个文件的名称，实例化一个文件对象
  File file = new File("file_name.txt");
  if (file.exits()) {    //判断文件是否存在
	//文件存在实例化一个InputStream流
    FileInputStream fis = new FileInputStream(file);
	//BufferedInputStream 能够提供缓存，将InputStream转化成BufferedInputStream
    scanner = new Scanner(new BufferedInputStream(fis),"UTF-8"); //假设是使用UTF-8进行编码
    scanner.useLocale(Locale.US);//assume language = English, country = US for consistency with System.Out
    //Scanner对象实例化完成
  }
} catch(IOException ioe) {
  throw nes IllegalArgumentException("could not open"+ file,ioe);
}
```

### __Scanner__ 的主要操作有：

```java
boolean hasNext() //判断还有没有下一个短语，如果有就返回True，可以作为判断输入流有没有内容的一个标志
String next() //返回下一个短语，并且Scanner向后短语移动一个，根据Scanner定义的delimiter来划分短语
int	nextInt() //返回下一个短语，短语的类型是int
String nextLine() //返回新的一行，并向后在移动一行
Scanner	useDelimiter(Pattern pattern) //根据设定的划分符号来划分短语
Scanner useDelimiter(String Pattern) 
Scanner useLocale(Locale locale) //设置相应的locale信息
```

对一个事例文件进行读写，文件形式如下：

```txt
0,a,one
1,b,two
2,c,three
```

假设我们要输出第1列所有内容，代码如下：

```java
//scanner之前已经实例化，只写读出第1列的代码
ArrayList<Integer> readFirst() {
  ArrayList<Integer> target = ArrayList<Integer>(); 
  String[] ind;
  while(scanner.hasNext()) {
    String line = scanner.readLine();
	ind = line.split(",");
    target.append(Integer.parseInt(ind[0]));
  }
  return target;
}
```

## In使用


[__In__](http://algs4.cs.princeton.edu/code/edu/princeton/cs/algs4/In.java.html) 是David Pritchard,Robert Sedgewick,Kevin Wayne几位的产品，在算法课上基本上是用这个类解决文件的读入读出，未进行实际的评测，但是在书中有使用其读入几十万条数据。

### __In__ 构造函数有

```java
public In() //通过standard input来构建一个inputStream
public In(Socket socket) //通过socket构建inputStream
public In(URL url) //通过url构建inputStream
public In(File file) //通过File构建inputStream
public In(String name) //Initializes an input stream from a filename or web page name
public In(Scanner scanner) // Initializes an input stream from a given source;
```

能我目前的满足全部需求，对于socket还是没有了解，具体的构造函数实现举一个例子：

```java
public In(File file) {
   if (file == null) throw new IllegalArgumentException("file argument is null");
        try {
            // for consistency with StdIn, wrap with BufferedInputStream instead of use
            // file as argument to Scanner
            FileInputStream fis = new FileInputStream(file);
            scanner = new Scanner(new BufferedInputStream(fis), CHARSET_NAME);
            scanner.useLocale(LOCALE);
        }
        catch (IOException ioe) {
            throw new IllegalArgumentException("Could not open " + file, ioe);
          //最开始不习惯加上throw这个功能，后来感觉如果读入有错误应该有地方能报错这是很明智的地方；
          //类似使用assert断言功能
        }
}
```

### __In__ 的具体操作

```java
public boolean isEmpty() // 和Scanner.hasNext()一样，判断是否还能继续往下读
public boolean hasNextLine() //和Scanner.hasNextLine()一样
public String readString() //Reads the next token from this input stream and returns it as a String
public int readInt() //使用Scanner.nextInt()来读入一个int
public String[] readAllLines() //读入所有的line，并将它们存储在array中
public int[] readAllInts() //读入所有int
public void close() //关闭scanner
```

__In__ 的这些操作主要是借用 __Scanner__ 的 __hasNext__ , __next__ , __nextInt__, __nextLine__ 等方法再结合 __arraylist__ 方法来存储输出那些切分好的片段。基于目前的认识感觉 __In__ 类使用方便，基于文件的读写中间很多过程隐藏了。





