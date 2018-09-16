java 性能优化之字符串处理
中对String连接的处理，单纯的使用+号来连接俩个字符串，是非常的耗费时间，效率教低，
相比较而言，可以使用StringBuffer来进行累加操作,而且还是线程安全的
    StringBuffer s1 = new StringBuffer();
    String s ="字符串"
    s1.append("s")

如果不考虑线程安全，可以考虑StringBuilder

(2) 对于基本类型转换成字符串,建议使用toString
例如 int m = 0;
String s = num.toString();
