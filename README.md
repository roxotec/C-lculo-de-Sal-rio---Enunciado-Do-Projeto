# C-lculo-de-Sal-rio---Enunciado-Do-Projeto

Faça um programa que receba 5 salários brutos de funcionários, sabendo-se que são descontados Imposto de Renda e INSS, calcule e mostre o total do salário líquido no referido mês.

Obs.: Salário Bruto - Descontos = Salário Líquido.

A saída do programa deve fornecer as seguintes informações:

Salário bruto.
Quanto pagou ao INSS.
Quanto pagou de Imposto de Renda.
Salário líquido.
Calcule os descontos e o salário líquido com base nas tabelas abaixo:

Salário	% Desconto INSS
até 1.212,00	7,5%
de 1212,01 até 2.427,35	9%
de 2.427,36 até 3.641,03	12%
de 3.641,04 até 7.087,22	14%
Salário	% Desconto Imposto de Renda
até 1.903,98	0%
de 1.903,99 até 2.826,65	7,5%
de 2.826,66 até 3.751,05	15%
de 3.751,06 até 4.664,68	22,50%
Acima de 4.664,68	27,50%

Resolução de codigo:

import java.util.Scanner;

public class CalculoSalario {
    
    public static double calcularINSS(double salario) {
        if (salario <= 1212.00) {
            return salario * 0.075;
        } else if (salario <= 2427.35) {
            return salario * 0.09;
        } else if (salario <= 3641.03) {
            return salario * 0.12;
        } else if (salario <= 7087.22) {
            return salario * 0.14;
        } else {
            return 7087.22 * 0.14; // Teto do INSS
        }
    }
    
    public static double calcularIR(double salario) {
        if (salario <= 1903.98) {
            return 0;
        } else if (salario <= 2826.65) {
            return salario * 0.075;
        } else if (salario <= 3751.05) {
            return salario * 0.15;
        } else if (salario <= 4664.68) {
            return salario * 0.225;
        } else {
            return salario * 0.275;
        }
    }
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        double[] salarios = new double[5];
        
        for (int i = 0; i < 5; i++) {
            System.out.print("Digite o salário bruto do funcionário " + (i + 1) + ": ");
            salarios[i] = scanner.nextDouble();
        }
        
        for (int i = 0; i < 5; i++) {
            double salarioBruto = salarios[i];
            double descontoINSS = calcularINSS(salarioBruto);
            double descontoIR = calcularIR(salarioBruto - descontoINSS); // IR é calculado após desconto do INSS
            double salarioLiquido = salarioBruto - descontoINSS - descontoIR;
            
            System.out.println("\nFuncionário " + (i + 1) + ":");
            System.out.printf("Salário bruto: R$ %.2f\n", salarioBruto);
            System.out.printf("Desconto INSS: R$ %.2f\n", descontoINSS);
            System.out.printf("Desconto IR: R$ %.2f\n", descontoIR);
            System.out.printf("Salário líquido: R$ %.2f\n", salarioLiquido);
        }
        
        scanner.close();
    }
}


