# Mermaid-Copilot_DataSaturday-2024-10
Materiais da apresentação "IA + Documentação em Bancos de Dados: utilizando GitHub Copilot + Mermaid para gerar diagramas". Palestra realizada durante o Data Saturday em Vitória-ES no dia 26/10/2024.

---

## Mindmap

Pergunta ao Copilot:

```
Gostaria de um mapa mental em Mermaid que traga tecnologias, tópicos e práticas que preciso estudar para conhecer mais sobre Data Analytics
```

Resposta:

```mermaid
mindmap
  root((Data Analytics))
    Tecnologias
      Python
      R
      SQL
      Excel
      PowerBI
      Tableau
    Tópicos
      Estatística
      Machine Learning
      Data Mining
      Data Cleaning
      Data Visualization
    Práticas
      Coleta de Dados
      Análise Exploratória
      Modelagem de Dados
      Validação de Modelos
      Comunicação de Resultados
```

---

## Entidade-Relacionamento

Gere um diagrama de entidade-relacionamento em Mermaid para o script:

```sql
CREATE DATABASE BaseDadosGeograficos
GO

USE BaseDadosGeograficos
GO

CREATE TABLE dbo.Regioes(
	IdRegiao int NOT NULL,
	CodRegiao varchar(2) NOT NULL,
	NomeRegiao varchar(20) NOT NULL,
	CONSTRAINT PK_Regioes PRIMARY KEY (IdRegiao)
)
GO

CREATE TABLE dbo.Estados(
	SiglaEstado char(2) NOT NULL,
	NomeEstado varchar(20) NOT NULL,
	NomeCapital varchar(20) NOT NULL,
	IdRegiao int NOT NULL,
	CONSTRAINT PK_Estados PRIMARY KEY (SiglaEstado),
	CONSTRAINT FK_Estado_Regiao FOREIGN KEY (IdRegiao) REFERENCES dbo.Regioes(IdRegiao)
)
GO
```

Resultado:

```mermaid
erDiagram
    Regioes {
        int IdRegiao PK
        varchar CodRegiao
        varchar NomeRegiao
    }

    Estados {
        char SiglaEstado PK
        varchar NomeEstado
        varchar NomeCapital
        int IdRegiao FK
    }

    Regioes ||--o{ Estados: "possui"
```

---

## Flowchart

Pergunta ao Copilot:

```
Como seria em um fluxograma do Mermaid uma rotina automatizada de backup do SQL Server?
```

Resultado:

```mermaid
graph TD
    A[Início] --> B[Verificar espaço em disco]
    B -->|Espaço suficiente| C[Conectar ao SQL Server]
    B -->|Espaço insuficiente| G[Enviar alerta de espaço insuficiente]
    C --> D[Iniciar backup]
    D --> E[Verificar integridade do backup]
    E -->|Sem problemas de integridade| F[Salvar backup e registrar log]
    E -->|Backup corrompido| H[Enviar alerta de falha no backup]
    F --> I[Fim]
    G --> I[Fim]
    H --> I[Fim]
```

---

## Diagrama de sequência

Pergunta ao Copilot:

```
Como seria um diagrama de sequência em Mermaid de um processo de ETL que usa arquivos do Excel como origem e que estão no Azure Storage, processando os dados via Azure Data Factory e consolidando isso numa base do Azure SQL?
```

Resposta:

```mermaid
sequenceDiagram
    actor Usuário
    participant AzureStorage as Azure Storage
    participant ADF as Azure Data Factory
    participant AzureSQL as Azure SQL Database

    Usuário->>AzureStorage: Upload arquivos Excel
    AzureStorage->>ADF: Notificação de novos arquivos
    ADF->>AzureStorage: Ler arquivos Excel
    ADF->>ADF: Processar dados (Transformação)
    ADF->>AzureSQL: Carregar dados transformados
    AzureSQL->>Usuário: Confirmação de dados carregados
```

## Diagrama de classes

Estrutura:

```csharp
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;
using System.Text.Json.Serialization;

namespace BenchmarkingDapperEFCoreCRMMySql.EFCore;

public class Empresa
{
    [Key]
    public int IdEmpresa { get; set; }
    public string? CNPJ { get; set; }
    public string? Nome { get; set; }
    public string? Cidade { get; set; }
    public List<Contato>? Contatos { get; set; }
}

public class Contato
{
    [Key]
    public int IdContato { get; set; }
    public string? Nome { get; set; }
    public string? Telefone { get; set; }

    [ForeignKey("IdEmpresa")]
    [JsonIgnore]
    public Empresa? EmpresaRepresentada { get; set; }
}
```

Resultado:

```mermaid
classDiagram
    class Empresa {
        int IdEmpresa
        string? CNPJ
        string? Nome
        string? Cidade
        List~Contato~? Contatos
    }

    class Contato {
        int IdContato
        string? Nome
        string? Telefone
        Empresa? EmpresaRepresentada
    }

    Empresa "1" --> "0..*" Contato : Contatos
```