import java.util.Scanner;

public class Calculator {
    public static void main(String[] args) {
        Converter converter = new Converter();
        String[] actions = {"+","-","/","*"};
        String[] regexActions = {"\\+", "-", "/", "\\*"};
        Scanner scn = new Scanner(System.in);
        System.out.print("Ваш пример: ");
        String exp = scn.nextLine();
        String []minus = exp.split("\\-");
        String []plus = exp.split("\\+");
        String []delit = exp.split("\\/");
        String []ymnog = exp.split("\\*");
        int collznacov = minus.length-1 + plus.length-1 + delit.length-1 + ymnog.length-1;
        if(collznacov > 1){
            System.out.println("формат математической операции не удовлетворяет заданию - два операнда и один оператор");
            return;
        }
        int value = exp.indexOf('.');
        int value1 = exp.indexOf(',');
        int play = value1+ value;
        if (play != -2){
            System.out.println("исключение, число должно быть целым");
            return;
        }
        int actionIndex=-1;
        for (int i = 0; i < actions.length; i++) {
            if(exp.contains(actions[i])){
                actionIndex = i;
                break;
            }
        }
        if(actionIndex==-1){
            System.out.println("Cтрока не является математической операцией");
            return;
        }

        String[] data = exp.split(regexActions[actionIndex]);
        if(converter.isRoman(data[0]) == converter.isRoman(data[1])){
            int a,b;
            boolean isRoman = converter.isRoman(data[0]);
            if(isRoman){
                a = converter.romanToInt(data[0]);
                b = converter.romanToInt(data[1]);
                if(a>10 || b > 10){
                    System.out.println("Числа не должны быть больше 10");
                    return;
                }

            }else{
                a = Integer.parseInt(data[0]);
                b = Integer.parseInt(data[1]);
                if(a>10 || b > 10){
                    System.out.println("Числа не должны быть больше 10");
                    return;
                }
            }

            int result;
            switch (actions[actionIndex]){
                case "+":
                    result = a+b;
                    break;
                case "-":
                    result = a-b;
                    break;
                case "*":
                    result = a*b;
                    break;
                default:
                    result = a/b;
                    break;
            }
            if(isRoman){
                if(result<0){
                    System.out.println("В римской системе нет отрицательных чисел");
                }
                else {
                    System.out.println(converter.intToRoman(result));
                }
            }
            else{
                System.out.println(result);
            }
        }else{
            System.out.println("Числа должны быть в одном формате");
        }
    }
}
