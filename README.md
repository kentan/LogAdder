#LogAdder
LogAdder is tools for analyzing Java code by adding log at the top of methods. </br>
Large and complex Java codes that uses asynchronous and multithreading technique make programmers to understand the flow.</br>
The LogAdder helps you to understand how the code is run by seeing the outputed log.</br>

# Getting Started
## Adding standard input to the beginning of all methods.

1. Prepare the java source code you would like to add log to.

 In this tutorial, we will add the log to the following java source code.
 ```java
    public class Target{
       public static void main(String[] args){
          step1();
          step2();
          step3();
       }
       public static void step1(){}
        
       public static void step2(){}
       
       public static void step3(){}
    }
 ```
2. Implement the following class.

 ```java
    public class StdOutAdder {
       public static void main(String args[]) {
            LogAdder logAdder = new  LogAdder();
            String filePath = "<File or Directory path of Target.java>";
            String message = "\"I\'m at \"+";
            String addingStatement = "System.out.println(" + message + "new Exception().getStackTrace()[0].toString());";
            try {
                Statement statement = JavaParser.parseStatement(addingStatement);
                logAdder.setLogStatement(statement);
                logAdder.addLog(filePath);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
 ```
3. Compile and execute the StdOutAdder.java.</br>

 As a result of the execusion, you will find the class Target has been changed to the following.
 ```java
public class Target{
   public static void main(String[] args){
      System.out.println("I'm at " + new Exception().getStackTrace()[0].toString());
      step1();
      step2();
      step3();
   }
    
   public static void step1(){
     System.out.println("I'm at " + new Exception().getStackTrace()[0].toString());
   }
    
   public static void step2(){
     System.out.println("I'm at " + new Exception().getStackTrace()[0].toString());
   }
    
   public static void step3(){
     System.out.println("I'm at " + new Exception().getStackTrace()[0].toString());
   }
}
 ```
4. Compile and execute the Target.

 You will get the following output.

>I'm at com.github.kentan.logadder.sample.data.Sample1.main(Sample1.java:6)</br>
>I'm at com.github.kentan.logadder.sample.data.Sample1.sample(Sample1.java:14)</br>
>I'm at com.github.kentan.logadder.sample.data.Sample1.sample2(Sample1.java:19)</br>
>I'm at com.github.kentan.logadder.sample.data.Sample2.sample(Sample2.java:6)</br>
>I'm at com.github.kentan.logadder.sample.data.Sample2.sample2(Sample2.java:11)</br>

#License
Offered under the GNU Lesser General Public License: COPYING.LESSER, COPYING.</br>
LogAdder uses JavaParser(https://github.com/javaparser/javaparser). </br>
