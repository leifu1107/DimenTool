# DimenTool
Android 屏幕适配方案,自动生成不同分辨率的值
android中官方建议的屏幕适配方式，通过根据不同的分辨率在工程的res文件夹下建立不同的尺寸文件夹，每个文件夹下都建立dimens.xml文件。然后根据不同的尺寸在dimens.xml文件夹中分别计算配置不同的dp或者sp单位。开发中发现，android屏幕适配需要用到很多的尺寸，每个尺寸都建立dimens.xml问价。每个文件中的数值都要按照比例去计算，一个一个拿着计算器去计算吗？这样太麻烦了。今天有一个好的办法，来为大家介绍一下。

#### 步骤
##### 1.在工程的java文件夹下把项目的DimenTool.java复制到该文件夹下。
![](https://github.com/leifu1107/DimenTool/raw/master/screenshots/2.png) 
```java
/**
 * Created by cdy on 2016/2/3. 
 * 快速生成适配工具类 ,直接运行不成功需手动放入目录文件中
 */
public class DimenTool {

    public static void gen() {
        //以此文件夹下的dimens.xml文件内容为初始值参照  
        File file = new File("./app/src/main/res/values/dimens.xml");

        BufferedReader reader = null;
        StringBuilder sw240 = new StringBuilder();
        StringBuilder sw320 = new StringBuilder();
        StringBuilder sw360 = new StringBuilder();
        StringBuilder sw480 = new StringBuilder();
        StringBuilder sw600 = new StringBuilder();
        StringBuilder sw720 = new StringBuilder();
        StringBuilder sw800 = new StringBuilder();
        StringBuilder w820 = new StringBuilder();

        try {

            System.out.println("生成不同分辨率：");

            reader = new BufferedReader(new FileReader(file));

            String tempString;

            int line = 1;

            // 一次读入一行，直到读入null为文件结束  

            while ((tempString = reader.readLine()) != null) {


                if (tempString.contains("</dimen>")) {

                    //tempString = tempString.replaceAll(" ", "");  

                    String start = tempString.substring(0, tempString.indexOf(">") + 1);

                    String end = tempString.substring(tempString.lastIndexOf("<") - 2);
                    //截取<dimen></dimen>标签内的内容，从>右括号开始，到左括号减2，取得配置的数字  
                    Double num = Double.parseDouble
                            (tempString.substring(tempString.indexOf(">") + 1,
                                    tempString.indexOf("</dimen>") - 2));

                    //根据不同的尺寸，计算新的值，拼接新的字符串，并且结尾处换行。  
                    sw240.append(start).append( num * 0.75).append(end).append("\r\n");

                    sw320.append(start).append( num * 1).append(end).append("\r\n");

                    sw360.append(start).append( num * 1.125).append(end).append("\r\n");

                    sw480.append(start).append(num * 1.5).append(end).append("\r\n");

                    sw600.append(start).append(num * 1.87).append(end).append("\r\n");

                    sw720.append(start).append(num * 2.25).append(end).append("\r\n");

                    sw800.append(start).append(num * 2.5).append(end).append("\r\n");

                    w820.append(start).append(num * 2.56).append(end).append("\r\n");



                } else {
                    sw240.append(tempString).append("");

                    sw320.append(tempString).append("");

                    sw360.append(tempString).append("");

                    sw480.append(tempString).append("");

                    sw600.append(tempString).append("");

                    sw720.append(tempString).append("");

                    sw800.append(tempString).append("");

                    w820.append(tempString).append("");

                }

                line++;

            }

            reader.close();
            System.out.println("<!--  sw240 -->");

            System.out.println(sw240);

            System.out.println("<!--  sw320 -->");

            System.out.println(sw320);

            System.out.println("<!--  sw360 -->");

            System.out.println(sw360);

            System.out.println("<!--  sw480 -->");

            System.out.println(sw480);

            System.out.println("<!--  sw600 -->");

            System.out.println(sw600);

            System.out.println("<!--  sw720 -->");

            System.out.println(sw720);

            System.out.println("<!--  sw800 -->");

            System.out.println(sw800);

            String sw240file = "./app/src/main/res/values-sw240dp/dimens.xml";

            String sw320file = "./app/src/main/res/values-sw320dp/dimens.xml";

            String sw360file = "./app/src/main/res/values-sw360dp/dimens.xml";

            String sw480file = "./app/src/main/res/values-sw480dp/dimens.xml";

            String sw600file = "./app/src/main/res/values-sw600dp/dimens.xml";

            String sw720file = "./app/src/main/res/values-sw720dp/dimens.xml";

            String sw800file = "./app/src/main/res/values-sw800dp/dimens.xml";

            String w820file = "./app/src/main/res/values-w820dp/dimens.xml";
            //将新的内容，写入到指定的文件中去  
            writeFile(sw240file, sw240.toString());

            writeFile(sw320file, sw320.toString());

            writeFile(sw360file, sw360.toString());

            writeFile(sw480file, sw480.toString());

            writeFile(sw600file, sw600.toString());

            writeFile(sw720file, sw720.toString());

            writeFile(sw800file, sw800.toString());

            writeFile(w820file, w820.toString());

        } catch (IOException e) {

            e.printStackTrace();

        } finally {

            if (reader != null) {

                try {

                    reader.close();

                } catch (IOException e1) {

                    e1.printStackTrace();

                }

            }

        }

    }


    /**
     * 写入方法 
     *
     */

    public static void writeFile(String file, String text) {

        PrintWriter out = null;

        try {

            out = new PrintWriter(new BufferedWriter(new FileWriter(file)));

            out.println(text);

        } catch (IOException e) {

            e.printStackTrace();

        }



        out.close();

    }
    public static void main(String[] args) {

        gen();

    }

}  
```

##### 2.
![](https://github.com/leifu1107/DimenTool/raw/master/screenshots/1.png) 
![](https://github.com/leifu1107/DimenTool/raw/master/screenshots/3.png) 
![](https://github.com/leifu1107/DimenTool/raw/master/screenshots/4.png) 
![](https://github.com/leifu1107/DimenTool/raw/master/screenshots/5.png) 
