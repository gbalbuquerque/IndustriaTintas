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

[Link do wiki detalhado](https://github.com/gbalbuquerque/IndustriaTintas/wiki)


## 🚀 Diagrama de Casos de Uso

Este diagrama mostra as principais funcionalidades do sistema e como os diferentes atores interagem com ele:

<img src='./assets/useCases.png'>

## 📝 Casos de Uso Detalhados

Abaixo, detalhamos cada caso de uso, mostrando o fluxo principal, fluxos alternativos, pré-condições e pós-condições.

### UC_01 - Monitorar Operação

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_01.png">
</details>

### UC_02 - Reverter Operação

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_02.png">
</details>

### UC_03 - Liberar Caminhões

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_03.png" >
</details>

### UC_04 - Gerar Relatórios

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_04.png" >
</details>

### UC_05 - Informar demanda de Produção

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_05.png" >
</details>

### UC_06 - UC_06 - Enviar ordens de produção

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_06.png">
</details>

### UC_07 - Enviar dados de produção

<details>
<summary>Clique para expandir</summary>
<img src="./assets/casosDetalhados/uc_07.png">
</details>

## 🧮 Diagrama de Classes

``` mermaid

classDiagram

    Operador --> Pessoa

    Operador --> Misturador : controla
    Operador --> Tanque : monitora
    Operador --> Valvula : opera
    Operador --> Bomba : controla
    Operador --> Sensor : consulta

    Misturador --> Tanque : mistura no
    Misturador --> Tinta : usa

    Tanque --> Tinta : armazena
    Tanque --> Sensor : usa

    Bomba --> Tanque : alimenta/esvazia
    Valvula --> Tanque : regula entrada/saída

    Sensor --> Tanque : mede
    Sensor --> Bomba : mede
    Sensor --> Valvula : mede

    PCP --> Operador : envia ordem
    PCP --> Misturador : ativa mistura

    SistemaComercial --> PCP : informa demanda

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
        IniciaProducao()
        EmiteRelatorio()
        ReverteOperacao()
        LiberaCaminhao()
        MonitoraOperacao()
    }

    class CentralDeMonitoramento{
        int capacidade
        autorizaOperador()
        recusaLogin()
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
    class

```

## 📌 Diagrama de Sequência

1. Monitorar Operação
2. Reverter Operação
3. Liberar Caminhões
4. Gerar Relatórios
5. Informar Demanda de Produção
6. Enviar ordens de produção
7. Enviar dados de produção


### 1️⃣ Operador que Monitorar Operação

```mermaid
sequenceDiagram


actor Operador
participant Central de Monitoramento
participant Sistema
participant Sensores

Operador->>Sistema: Acessa sistema
Sistema->>Operador: Solicita autenticação
Operador->>Sistema: Fornece credenciais

alt Credenciais válidas
    Sistema->>Sistema: Valida acesso
    Sistema->>Operador: Exibe painel de status

    loop Atualização contínua
        Sensores->>Sistema: Dados de pressão/nível
        Sistema->>Central de Monitoramento: Encaminha dados
        Sistema->>Operador: Atualiza indicadores
    end
else Credenciais inválidas 
    Sistema->>Operador: Nega acesso
    Sistema->>Operador: Exibe mensagem de erro
end

alt Falha na comunicação 
    Sensores->>Sistema: Sem dados
    Sistema->>Central de Monitoramento: Notifica falha
    Sistema->>Operador: Exibe mensagem de alerta
end
```
### 2️⃣ Reverter Operação

```mermaid
sequenceDiagram
    
    actor Operador
    participant Central de Monitoramento
    participant Sistema

    Operador->>Central de Monitoramento: Acessa painel
    Central de Monitoramento->>Sistema: Solicita interface
    Sistema->>Central de Monitoramento: Exibe operações em andamento
    Central de Monitoramento->>Operador: Exibe interface

    Operador->>Sistema: Seleciona operação e solicita reversão

    alt Operação em estágio reversível
        Sistema->>Sistema: Verifica estágio da operação
        Sistema->>Sistema: Inicia processo de parada segura
        Sistema->>Operador: Confirma reversão finalizada
    else Operação irreversível
        Sistema->>Operador: Exibe mensagem de alerta
        Operador->>Sistema: Retorna à tela principal
    end
```
### 3️⃣ Liberar Caminhões

```mermaid
sequenceDiagram
   actor Operador
    participant Central de Monitoramento
    participant Sistema
    participant Caminhão

    Operador->>Central de Monitoramento: Acessa sistema
    Central de Monitoramento->>Sistema: Solicita dados dos tanques
    Sistema->>Central de Monitoramento: Exibe níveis dos tanques
    Central de Monitoramento->>Operador: Mostra níveis

    Operador->>Sistema: Identifica tanques próximos do limite
    Operador->>Sistema: Autoriza liberação do caminhão

    alt Caminhão disponível
        Sistema->>Caminhão: Inicia esvaziamento
        Caminhão->>Sistema: Confirma esvaziamento concluído
        Sistema->>Operador: Finaliza processo
    else Caminhões indisponíveis [FS001]
        Sistema->>Operador: Exibe alerta
    end

```
### 4️⃣ Gerar Relatório

```mermaid
sequenceDiagram

    actor Operador
    participant Sistema
    participant Banco de Dados

    Operador->>Sistema: Acessa módulo de relatórios
    Operador->>Sistema: Realiza consulta com filtros

    alt Filtros válidos
        Sistema->>Banco de Dados: Consulta dados conforme filtros
        Banco de Dados->>Sistema: Retorna dados
        Sistema->>Operador: Exibe relatório
        Operador->>Sistema: Solicita exportação em PDF/CSV
        Sistema->>Operador: Disponibiliza arquivo para download
    else [FS001] Filtros inválidos ou sem resultado
        Sistema->>Operador: Exibe mensagem de que não há dados
    end

```

### 5️⃣ Informar Demanda de Produção
```mermaid
sequenceDiagram

    participant Sistema_Comercial
    participant Sistema_de_Controle
    participant Operador

    Sistema_Comercial->>Sistema_Comercial: Identifica novo pedido de venda
    Sistema_Comercial->>Sistema_de_Controle: Envia dados do pedido (produto, quantidade, prazo)
    Sistema_de_Controle->>Sistema_de_Controle: Registra demanda de produção
    Sistema_de_Controle->>Operador: Exibe notificação de nova demanda

```
### 6️⃣ Enviar Ordens de Produção
```mermaid
sequenceDiagram

    participant Sistema_de_Controle
    participant Sistema_PCP

    Sistema_de_Controle->>Sistema_de_Controle: Agrupa demandas por tipo e prioridade
    Sistema_de_Controle->>Sistema_de_Controle: Gera ordem de produção (lote, quantidade, parâmetros técnicos)
    Sistema_de_Controle->>Sistema_PCP: Envia ordem de produção
    Sistema_PCP-->>Sistema_de_Controle: Confirma recebimento da ordem

```
### 7️⃣ Enviar Dados de Produção
```mermaid

sequenceDiagram

    participant Sensores
    participant Sistema_de_Controle
    participant Operador

    Sensores->>Sistema_de_Controle: Captura e envia dados do processo [FS001]
    loop Periódico
        Sensores->>Sistema_de_Controle: Envia dados (pressão, nível)
    end
    Sistema_de_Controle->>Sistema_de_Controle: Atualiza status dos tanques e equipamentos
    Sistema_de_Controle-->>Operador: Exibe andamento da produção em tempo real

    alt FS001 - Falha nos sensores
        Sensores-->>Sistema_de_Controle: Falha na transmissão de dados
        Sistema_de_Controle-->>Operador: Exibe alerta de falha no sensor
    end


```

## 📈 Diagrama de Estados

### 1️⃣ Operador
```mermaid
stateDiagram
    [*] --> IniciaProducao() : Se login e senha estiverem corretos
    IniciaProducao() --> MonitoraOperacao() : Se a operacao tiver sido iniciada
    MonitoraOperacao() --> LiberarCaminhao() : Se estiver tudo certo
    MonitoraOperacao() --> ReverterOperacao() : Se acontecer algum empecilho
    ReverterOperacao() --> IniciaProducao()
    LiberarCaminhao() --> GerarRelatorios() : Caminhões abastecidos
    LiberarCaminhao() -->  MonitoraOperacao : Caminhçao sem o carregamento completo
    GerarRelatorios() --> [*]
```

### 3️⃣ Central de Monitoramento
```mermaid
stateDiagram
    [*] --> : Se a credencial estiver correta
    
```
### 4️⃣ Sistema Comercial
```mermaid
stateDiagram
    [*] --> InformarDemanda() : Se a quantidade da demanda for estabelecida
    InformarDemanda() --> [*]

``` 

### 5️⃣ Sistema Controle Tintas
```mermaid
stateDiagram-v2
    [*] --> Ocioso_AguardandoEntrada

    Ocioso_AguardandoEntrada --> RecebendoDadosExternos : [Nova ordem do PCP/Comercial (UC_05) ou Dados de Sensores (UC_07)]
    Ocioso_AguardandoEntrada --> RecebendoComandoDaCentralMonitoramento : [Operador solicita ação via UI (UC_01, UC_02, UC_03, UC_04, Seq. Iniciar Prod.)]

    RecebendoDadosExternos --> ProcessandoDadosRecebidos : [Validar ordem, registrar dados de sensor]
    ProcessandoDadosRecebidos --> AtualizandoEstadoInterno_E_NotificandoUI : [Ordem na fila, painel atualizado com dados de sensor]
    AtualizandoEstadoInterno_E_NotificandoUI --> Ocioso_AguardandoEntrada

    RecebendoComandoDaCentralMonitoramento --> ValidandoEProcessandoComandoOperador : [Verificar permissões, estado da linha]
    ValidandoEProcessandoComandoOperador --> ExecutandoAcaoRequisitada : [Iniciar/Parar produção, abrir/fechar válvula, gerar dados de relatório]
    ExecutandoAcaoRequisitada --> EnviandoRespostaOuConfirmacaoParaCentralMonitoramento
    EnviandoRespostaOuConfirmacaoParaCentralMonitoramento --> Ocioso_AguardandoEntrada : [Comando concluído]

    Ocioso_AguardandoEntrada --> [*] : [Desligamento do sistema, não usual]
```

### 6️⃣ Módulo Interface Sensores
```mermaid
stateDiagram-v2
    [*] --> RecebendoDadoBrutoDoHardwareSensor
    RecebendoDadoBrutoDoHardwareSensor --> ProcessandoDadoBrutoSensor : [validação, conversão, etc.]
    ProcessandoDadoBrutoSensor --> ReportandoDadoProcessadoAoSistemaControle : [dado válido]
    ProcessandoDadoBrutoSensor --> ReportandoFalhaDeLeituraAoSistemaControle : [erro na leitura/processamento]
    ReportandoDadoProcessadoAoSistemaControle --> AguardandoProximoCicloDeLeitura
    ReportandoFalhaDeLeituraAoSistemaControle --> AguardandoProximoCicloDeLeitura
    AguardandoProximoCicloDeLeitura --> [*]
```
## 🎱 Diagramas de Atividades
### Interface de Produção
```mermaid
graph TD
    start([Início - Nova Ordem de Produção])

    subgraph "Sistema PCP"
        pcpA1[Gera Ordem de Produção - produto, quantidade]
        pcpA2[Envia Ordem para Sistema de Controle de Tintas]
    end

    subgraph "Operador (Central de Monitoramento)"
        opB1[Visualiza Ordem Pendente no painel]
        opB2[Verifica disponibilidade de matéria-prima e linha]
        opB3[Seleciona Ordem e Inicia Produção via Central]
        opB4[Monitora processo - níveis, pressões, status equipamentos]
        opB5{"Intervenção Necessária?"}
        opB6[Realiza ajuste manual ou aciona parada de emergência]
        opB7[Confirma conclusão do lote no painel]
    end

    subgraph "Sistema de Controle da Linha de Tintas"
        sysC1[Recebe Ordem do PCP e registra]
        sysC2[Notifica Operador sobre nova Ordem via Central]
        sysC3[Recebe comando de Início de Produção da Central]
        sysC4[Carrega receita e parâmetros da Ordem]
        sysC5[Comanda dosagem de bases - bombas B1/B2, válvulas V1/V2]
        sysC6[Monitora sensores de dosagem de bases]
        sysC7[Comanda dosagem de corantes - válvulas V3-V8]
        sysC8[Monitora sensores de dosagem de corantes]
        sysC9[Comanda mistura em M1/M2]
        sysC10[Monitora processo de mistura]
        sysC11[Comanda transferência para Tanque Armazenamento E7-E13 via V9-V16]
        sysC12[Monitora nível do tanque de destino]
        sysC13[Registra lote como concluído e atualiza status]
        sysC14[Notifica Operador sobre conclusão via Central]
        sysC15[Processa comandos de intervenção do Operador]
    end

    start --> pcpA1
    pcpA1 --> pcpA2
    pcpA2 --> sysC1
    sysC1 --> sysC2
    sysC2 --> opB1
    opB1 --> opB2
    opB2 --> opB3
    opB3 --> sysC3
    sysC3 --> sysC4
    sysC4 --> sysC5
    sysC5 --> sysC6
    sysC6 --> sysC7
    sysC7 --> sysC8
    sysC8 --> sysC9
    sysC9 --> sysC10
    sysC10 --> sysC11
    sysC11 --> sysC12
    sysC12 --> opB4
    opB4 --> opB5
    opB5 -- Sim --> opB6
    opB6 --> sysC15
    sysC15 --> opB4
    opB5 -- Não --> sysC13
    sysC13 --> sysC14
    sysC14 --> opB7
    opB7 --> end_producao([Fim - Lote Produzido])
```
### Processo de esvaziation
```mermaid
graph TD
    start_esvaziamento([Início - Necessidade de Esvaziar Tanque])

    subgraph "Operador (Central de Monitoramento)"
        opD1[Identifica Tanque com produto pronto para esvaziar]
        opD2[Verifica se caminhão está posicionado/disponível]
        opD3[Comanda Liberação do Tanque para Esvaziamento via Central]
        opD4[Monitora nível do tanque durante esvaziamento]
        opD5[Confirma finalização do esvaziamento ou interrupção]
    end

    subgraph "Sistema de Controle da Linha de Tintas"
        sysE1[Recebe comando de Liberação de Tanque da Central]
        sysE2[Verifica status do tanque - nível, tipo de produto]
        sysE3[Comanda abertura da válvula de saída do tanque selecionado]
        sysE4[Envia dados de nível do tanque para Central de Monitoramento]
        sysE5{"Tanque Vazio ou Caminhão Cheio?"}
        sysE6[Comanda fechamento da válvula de saída do tanque]
        sysE7[Registra esvaziamento e atualiza status do tanque]
        sysE8[Notifica Central sobre finalização/status]
    end

    subgraph "Logística/Caminhão (Entidade Externa)"
        logF1[Caminhão se posiciona para carregamento]
        logF2[Inicia recebimento de tinta]
        logF3[Sinaliza que está cheio ou que o tanque esvaziou]
    end

    start_esvaziamento --> opD1
    opD1 --> opD2
    opD2 --> logF1
    logF1 --> opD3
    opD3 --> sysE1
    sysE1 --> sysE2
    sysE2 --> sysE3
    sysE3 --> logF2
    logF2 --> opD4
    sysE3 --> sysE4
    sysE4 --> opD4
    opD4 --> sysE5
    sysE5 -- Sim --> sysE6
    sysE6 --> sysE7
    sysE7 --> sysE8
    sysE8 --> opD5
    logF3 --> opD5
    opD5 --> end_esvaziado([Fim - Esvaziamento Concluído/Interrompido])
```

## 🖥️ Diagramas de Componentes e Integração
```mermaid
graph TD
    subgraph "Sistema de Controle da Linha de Tintas - Componentes"
        %% Aplicações de Interface
        CentralMonitoramento_UI[<<application>><br>Interface Central Monitoramento<br>Desktop App / Web App]

        %% Núcleo do Sistema de Controle (Backend)
        subgraph "<<service>> ServicoControleTintas.jar/.war"
            direction LR
            APIGestaoOrdens[API Gestão de Ordens]
            MotorControleProcesso[Motor de Controle de Processo]
            LogicaReceitasFormulas[Lógica de Receitas e Fórmulas]
            ModuloRelatorios[Módulo de Geração de Relatórios]
            ModuloSegurancaAlarmes[Módulo de Segurança e Alarmes]
        end

        %% Componentes de Integração e Drivers
        IntegracaoPCP_Comercial[<<component>><br>Adaptador API PCP/Comercial]
        DriverComunicacaoCLP[<<component>><br>Driver Comunicação CLP<br>OPC UA, Modbus, etc.]

        %% Persistência
        BancoDeDadosProducao[<<database>><br>BD Produção Tintas<br>Ordens, Receitas, Logs, Estoque]

        %% Dependências Internas
        CentralMonitoramento_UI --> APIGestaoOrdens
        CentralMonitoramento_UI --> MotorControleProcesso
        %% Para comandos manuais e visualização
        CentralMonitoramento_UI --> ModuloRelatorios
        CentralMonitoramento_UI --> ModuloSegurancaAlarmes

        APIGestaoOrdens --> LogicaReceitasFormulas
        APIGestaoOrdens --> MotorControleProcesso
        APIGestaoOrdens --> BancoDeDadosProducao

        MotorControleProcesso --> LogicaReceitasFormulas
        MotorControleProcesso --> DriverComunicacaoCLP
        %% Comanda os CLPs
        MotorControleProcesso --> ModuloSegurancaAlarmes
        MotorControleProcesso --> BancoDeDadosProducao
        %% Para log de eventos de processo

        LogicaReceitasFormulas --> BancoDeDadosProducao
        ModuloRelatorios --> BancoDeDadosProducao
        ModuloSegurancaAlarmes --> BancoDeDadosProducao
        ModuloSegurancaAlarmes --> MotorControleProcesso
        %% Pode enviar comandos de parada

        %% Dependências com Interfaces Externas
        APIGestaoOrdens --> IntegracaoPCP_Comercial
        %% Para receber ordens e talvez enviar status

    end

    %% Sistemas Externos
    CLPs_LinhaProducao("<<hardware>><br>CLPs da Linha de Produção")
    SistemaPCP_Externo("<<external_system>><br>Sistema PCP/Comercial")
    SensoresAtuadores("<<hardware>><br>Sensores e Atuadores da Linha")

    %% Conexões com Sistemas Externos
    DriverComunicacaoCLP -.-> CLPs_LinhaProducao
    IntegracaoPCP_Comercial -.-> SistemaPCP_Externo
    CLPs_LinhaProducao -.-> SensoresAtuadores
    %% CLPs leem sensores e comandam atuadores
```
## 🛠️ Tecnologias

*   **Diagramas:** ![Draw.io](https://img.shields.io/badge/draw.io-diagrams.net-orange?logo=drawio&logoColor=white)
*   **Diagramas de Caso de Uso:** ![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?logo=microsoft-excel&logoColor=white)
*   **Diagramas de Classes:** ![Mermaid](https://img.shields.io/badge/Mermaid-Diagram-blue?logo=mermaid&logoColor=white)
*   **Diagrama de Sequência:** ![Mermaid](https://img.shields.io/badge/Mermaid-Diagram-blue?logo=mermaid&logoColor=white)

---

## 🤝 Contribuições
Contribuições para aprimorar este projeto são muito bem-vindas, forke o projeto e contribua!

## ✉️ Contato
Qualquer dúvida sobre o projeto entrar em contato, será um prazer!
