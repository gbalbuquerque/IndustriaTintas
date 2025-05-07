# 🖌️🎨  Indústria de Tintas : Sistema de Gestão de Produção

[![Status do Projeto](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow)](https://shields.io/)


## 🌟 Equipe de Desenvolvimento

Uma equipe dedicada a transformar o controle de locações da VL!

*   **Bruno Basso** ➔ 22.123.067-5
*   **Gabriel Balbine** ➔ 22.222.001-4
*   **Gabriela Ciocci** ➔ 22.222.032-9
*   **Guilherme Albuquerque** ➔ 22.224.024-4

---

## 📖 Sobre o Projeto

Uma indústria de produção em massa de tintas, nos contratou para modernizar sua gestão!  Atualmente, a empresa opera com processos manuais e registros em fichas.  Nosso desafio é criar um sistema que automatize e otimize todas as etapas da produção.

## 🚀 Diagrama de Casos de Uso

Este diagrama mostra as principais funcionalidades do sistema e como os diferentes atores interagem com ele:

<img src='./assets/useCases.png'>

## 📝 Casos de Uso Detalhados

Abaixo, detalhamos cada caso de uso, mostrando o fluxo principal, fluxos alternativos, pré-condições e pós-condições.

### UC_01 - Monitorar Operação

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_01.png" alt="UC_01 - Monitorar Operação">
</details>

### UC_02 - Reverter Operação

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_02.png" alt="UC_02 - Reverter Operação">
</details>

### UC_03 - Liberar Caminhões

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_03.png" alt="UC_03 - Liberar Caminhões">
</details>

### UC_04 - Gerar Relatórios

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_04.png" alt="UC_04 - Gerar Relatórios">
</details>

### UC_05 - Informar demanda de Produção

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_05.png" alt="UC_05 - Informar demanda de Produção">
</details>

### UC_06 - UC_06 - Enviar ordens de produção

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_06.png" alt="UC_06 - Enviar ordens de produção">
</details>

### UC_07 - Enviar dados de produção

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_07.png" alt="UC_07 - Enviar dados de produção">
</details>

## 🧮 Diagrama de Classes

``` mermaid

classDiagram

classDiagram


    class Pessoa {
        String nome
        string nome
        long CPF
        data nascimento
        int idade
        VerificaCPF()
    }

    class Operador{
        String e-mail
        String senha
        EmiteRelatorio()
        ReverteOperacao()
        LiberaCaminhao()
        MonitoraOperacao()
    }

    class Misturador {
        String ID
        Boolean ativo
        MisturaCor()
    }

    class Bomba {
        String ID
        ControlaVazao()
    }

    class Valvula {
        Boolean vazamento
        Boolean ativo
        AbreFecha()
    }

    class Tanque {
        String ID
        float nivel
        armazenar()
        esvaziar()
    }

    class Sensor {
        float pressao
        float nivel
        float valor
        lerValor()
    }

    class Tinta {
        String cor
        float volume
    }

    class PCP {
        enviaOrdemProducao()
    }

    class SistemaComercial {
        informarDemanda()
    }



```
