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

enum INSS {
    FaixaSalarial1(1212.00, 7.5),
    FaixaSalarial2(2427.36, 9.0),
    FaixaSalarial3(3641.04, 12.0),
    FaixaSalarial4(Double.MAX_VALUE, 14.0);

    private final double salario;
    private final double taxa;

    INSS(double salario, double taxa) {
        this.salario = salario;
        this.taxa = taxa;
    }

    public double getTaxa() {
        return taxa;
    }

    public double getSalario() {
        return salario;
    }
}

enum ImpostoDeRenda {
    FaixaSalarial1(1903.98, 0),
    FaixaSalarial2(2826.65, 7.5),
    FaixaSalarial3(3751.05, 15.0),
    FaixaSalarial4(4664.68, 22.5),
    FaixaSalarial5(Double.MAX_VALUE, 27.5);

    private final double salario;
    private final double taxa;

    ImpostoDeRenda(double salario, double taxa) {
        this.salario = salario;
        this.taxa = taxa;
    }

    public double getTaxa() {
        return taxa;
    }

    public double getSalario() {
        return salario;
    }
}

public class CalculadoraSalario {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Digite o primeiro salário bruto:");
        double salario1 = scanner.nextDouble();
        ProcessarSalario(salario1);

        System.out.println("Digite o segundo salário bruto:");
        double salario2 = scanner.nextDouble();
        ProcessarSalario(salario2);

        System.out.println("Digite o terceiro salário bruto:");
        double salario3 = scanner.nextDouble();
        ProcessarSalario(salario3);

        System.out.println("Digite o quarto salário bruto:");
        double salario4 = scanner.nextDouble();
        ProcessarSalario(salario4);

        System.out.println("Digite o quinto salário bruto:");
        double salario5 = scanner.nextDouble();
        ProcessarSalario(salario5);

        scanner.close();
    }

    private static void ProcessarSalario(double salarioBruto) {
        double descontoINSS = CalcularINSS(salarioBruto);
        double descontoIR = CalcularImpostoDeRenda(salarioBruto - descontoINSS);
        double salarioLiquido = salarioBruto - descontoINSS - descontoIR;

        System.out.printf("Salário Bruto: %.2f\n", salarioBruto);
        System.out.printf("Desconto INSS: %.2f\n", descontoINSS);
        System.out.printf("Desconto IR: %.2f\n", descontoIR);
        System.out.printf("Salário Líquido: %.2f\n\n", salarioLiquido);
    }

    private static double CalcularINSS(double salario) {
        if (salario <= INSS.FaixaSalarial1.getSalario()) {
            return salario * INSS.FaixaSalarial1.getTaxa() / 100;
        } else if (salario <= INSS.FaixaSalarial2.getSalario()) {
            return salario * INSS.FaixaSalarial2.getTaxa() / 100;
        } else if (salario <= INSS.FaixaSalarial3.getSalario()) {
            return salario * INSS.FaixaSalarial3.getTaxa() / 100;
        } else {
            return salario * INSS.FaixaSalarial4.getTaxa() / 100;
        }
    }

    private static double CalcularImpostoDeRenda(double salario) {
        if (salario <= ImpostoDeRenda.FaixaSalarial1.getSalario()) {
            return salario * ImpostoDeRenda.FaixaSalarial1.getTaxa() / 100;
        } else if (salario <= ImpostoDeRenda.FaixaSalarial2.getSalario()) {
            return salario * ImpostoDeRenda.FaixaSalarial2.getTaxa() / 100;
        } else if (salario <= ImpostoDeRenda.FaixaSalarial3.getSalario()) {
            return salario * ImpostoDeRenda.FaixaSalarial3.getTaxa() / 100;
        } else if (salario <= ImpostoDeRenda.FaixaSalarial4.getSalario()) {
            return salario * ImpostoDeRenda.FaixaSalarial4.getTaxa() / 100;
        } else {
            return salario * ImpostoDeRenda.FaixaSalarial5.getTaxa() / 100;
        }
    }
}

