# java17
java Data 类Api分析
日期类【直到怎么查，怎么用即可，不用每个方法都被】
1.Date：精确到毫秒，代表特定的孙坚
2.SimpleDateFormat：格式和解析日期的类
SimpleDateFormat格式化和解析日期的具体类。它允许进行格式化（日期->文本）、解析（文本->日期）和规范化。
3.应用实例Date.java

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.SimpleTimeZone;

/**
 * @author 郑道炫
 * @version 1.0
 */
public class Date01 {
    public static void main(String[] args) throws ParseException {//抛出转换异常
        Date date = new Date();//获取当前日期时间
        System.out.println(date);//国外方式的时间

//      Date date1 = new Date(995959);
//      System.out.println(date1.getTime());
        //指定相应的格式，年y 月M 日d   h小时m分s秒 E天数
        SimpleDateFormat src = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss E");

        String format = src.format(date);
        System.out.println("当前日期=" + format);
        //1.可以吧一个格式化的String转成对应的Date
        //2.得到Date 仍然在输出时，还是按照国外的形式，如果希望指定格式输出，需要转换
        //3.
        String s ="1996年06月01日 10:20:55 星期一";
        Date parse = src.parse(s);
        System.out.println("parse=" + src.format(parse));



    }
//IDEA属性
}
class Date2{
    public static void main(String[] args) {
        Date date = new Date();
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM/dd hh:mm:ss E ");
        String format = simpleDateFormat.format(date);
        System.out.println(format);

    }
}
第二代日期类

1.主要就是Calendar类（日历）
public abstract class Calendar extends Object implements Serializable,Cloneable,Comparable<Calendar>
2.Calendar 类是一个抽象类，它为特定瞬间与一组诸如YEAR、MONTH、DAY_OF_MONTH、HOUT等日历字段之间的转换提供了一些方法，并为操作日历字段（例如获得下星期的日期）提供了一些方法。


import java.util.Calendar;

/**
 * @author 郑道炫
 * @version 1.0
 */
public class Calendar01 {
    /**
     *
     第二代日期类

     1.主要就是Calendar类（日历）
     public abstract class Calendar extends Object implements Serializable,Cloneable,Comparable<Calendar>
     2.Calendar 类是一个抽象类，它为特定瞬间与一组诸如YEAR、MONTH、DAY_OF_MONTH、HOUT等日历字段之间的转换提供了一些方法，并为操作日历字段（例如获得下星期的日期）提供了一些方法。
     */


    public static void main(String[] args) {
        //Calendar是一个抽象类，并且构造器是private
        //可以通过getInstance()来获取实例
        //提供大量的方法和字段提供给程序员
        //Calendar  //Calendar没有提供对应的格式化的类，incident需要程序员自己组合来输出
        //如果我们需要按照24小时进制来获取时间。改成HOUR Of Date
        Calendar i = Calendar.getInstance();//Calendar 是new不起来创建日历类对象
//        System.out.println(i);
        //获取日历对象的某个日历字段
        System.out.println("年：" + i.get(Calendar.YEAR));
         //这里为什么要+1，因为Calendar 返回月的时候，是按照 0开始编号的
        System.out.println("月：" + i.get(Calendar.MONTH));
        System.out.println("日：" + i.get(Calendar.DATE));
        System.out.println("小时" + i.get(Calendar.HOUR));
        System.out.println("分钟" + i.get(Calendar.MINUTE));
        System.out.println("秒" + i.get(Calendar.SECOND));
       System.out.println(i.get(Calendar.HOUR_OF_DAY));
    }
}年：2021
月：11
日：10
小时5
分钟22
秒0



=============================
第三代日期类
JDK1.0中包含了一个java.util.Date类，但是它的 大多数方法已经在JDK1.1引入Calendar类之后被启用了。而Calendar也存在的问题是：
1.可变性：像日期和时间这样的类应该是不可变的。
2.偏移性：Date中的年份是从1900开始的，而月份都从0开始。
3.格式化：格式化只对Date有用，Calendar则不行
4.此外，它们也不是线程安全；不能处理闰秒等（每隔2天，多出1s）。

第三代日期类常见方法
1.LocalDate（日期）、LocalTime（时间）、LocalDateTime（日期时间）JDK8加入
LocalDate只包含日期，可以获取日期字段
LocalTime只包含时间，可以获取时间字段
LocalDateTime包含日期+时间，可以获取日期和时间字段
案例演示

import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;

/**
 * @author 郑道炫
 * @version 1.0
 */
public class LocalDate_ {
    public static void main(String[] args) {
        //第三代日期
        //老韩解读
        //1.使用now（）返回当前日期时间的 兑现
        LocalDateTime now = LocalDateTime.now();
        System.out.println(now);
        System.out.println(now.getYear());
        System.out.println(now.getHour());
        System.out.println(now.getMonth());
        System.out.println(now.getMonthValue());
        LocalDate now2 = LocalDate.now();//获取年月日
        LocalTime now3 = LocalTime.now();//到时分秒


    }
2.DateTimeFormatter格式日期类
类似于SimpleDateFormat
DateTimeFormat dtf = DateTimeFormatter.ofPattern(格式);
String str = dtf.format(日期对象);
案例


import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;

/**
 * @author 郑道炫
 * @version 1.0
 */
public class LocalDate_ {
    public static void main(String[] args) {
        //第三代日期
        //老韩解读
        //1.使用now（）返回当前日期时间的 兑现
        LocalDateTime now = LocalDateTime.now();
        System.out.println(now);
        System.out.println(now.getYear());
        System.out.println(now.getHour());
        System.out.println(now.getMonth());
        System.out.println(now.getMonthValue());
        LocalDate now2 = LocalDate.now();//获取年月日
        LocalTime now3 = LocalTime.now();//到时分秒

//2.首映DateTimeFormatter 对象来进行格式化
        //创建DateTimeFormatter对象
        DateTimeFormatter srr = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH小时mm分钟ss秒");
        String format = srr.format(now);
        System.out.println("格式化的日期" + format);


=========================


3.Instant时间戳
类似于Date
提供了一系列和Date类转换的方式
Instance-------->Date:
Date date =Date.from(instant);
Date--------->Instant:
Instant instant = date.toInstant();
案例演示
Instant now = Instant.now();
System.out.println(now);
Date date = Date.from(now);
Instant instant = date.toInstant();



import java.time.Instant;
import java.util.Date;

/**
 * @author 郑道炫
 * @version 1.0
 */
public class Instant_ {
    public static void main(String[] args) {
//        System.out.println(java.time.Instant.now());

   //通过，静态方法now() 获取表示当前时间戳的对象
        Instant now = Instant.now();
        System.out.println(now);
        //通过from可以把 Instant转成Date
        Date date = Date.from(now);
        //通过date的toInstant()可以把date转成instant对象
        Instant instant = date.toInstant();
        System.out.println(instant);
    }



}
4.第三代日期类更多方法
LocalDateTime类
MothDay类：检查重复时间
是否是闰年
增加日期的某个部分
使用plus方法测试增加时间的某个部分
使用minus方法测试查import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;

/**
 * @author 郑道炫
 * @version 1.0
 */
public class LocalDate_ {
    public static void main(String[] args) {
        //第三代日期
        //老韩解读
        //1.使用now（）返回当前日期时间的 兑现
        LocalDateTime now = LocalDateTime.now();
    
//2.首映DateTimeFormatter 对象来进行格式化
        //创建DateTimeFormatter对象
        DateTimeFormatter srr = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH小时mm分钟ss秒");
        String format = srr.format(now);
        System.out.println("格式化的日期" + format);
        //提供plus和minus方法可以对当前时间进行操作
        //看看890天后，是什么时候 把 年 月 日 时 分 秒
        LocalDateTime local=now.plusHours(20000);
        System.out.println("过了200000天以后=" + srr.format(local));


        //看看在8000000分钟前，把年月日-时分钟输出
        LocalDateTime minus = now.minusMinutes(8000000);
        System.out.println("8000000分钟前=" + srr.format(minus));

    }

}
看一年前和一年后的日期
格式化的日期2021年12月10日 18小时51分钟09秒
过了200000天以后=2024年03月23日 02小时51分钟09秒
8000000分钟前=2006年09月25日 05小时31分钟09秒

Process finished with exit code 0




