
# Análise de Readmissão e Mortalidade por Artrite Séptica no SIH/SUS (2014-2023)

Este repositório contém o código Python utilizado para as análises apresentadas no artigo:

**Título do Artigo:** "Fatores associados à readmissão hospitalar e mortalidade por artrite séptica no Sistema Único de Saúde, Brasil, 2014-2023"
**Periódico (Submetido/Publicado):** Revista Epidemiologia e Serviços de Saúde (RESS)
**DOI da Publicação (se disponível):** [Inserir DOI do artigo quando publicado]

## INFORMAÇÕES GERAIS

* **Autores do Estudo/Código:**
    * **Investigador Principal/Contato:**
        * Nome: Jéssica Rodrigues Pereira
        * ORCID: https://orcid.org/0000-0003-2694-2445
        * Instituição: Hospital Municipal Padre Germano Lauck - Foz do Iguaçu, Paraná, Brasil
        * Email: drajessicarodriguesp@gmail.com
    * **Co-autor/Contato:**
        * Nome: Bruno Clavijo
        * ORCID: https://orcid.org/0009-0002-3239-1862
        * Instituição: Hospital Municipal Padre Germano Lauck - Foz do Iguaçu, Paraná, Brasil
        * Email: brunoclavijo@hotmail.com
    * **(Listar demais autores e informações)**
        * Nome: Lígia de Araújo Silva; ORCID: https://orcid.org/0009-0007-9714-4420; Email: draligiaaraujosilva@gmail.com
        * Nome: Moysés Mendes Gomes; ORCID: https://orcid.org/0009-0009-4616-088X; Email: moysesmendesgomes@gmail.com
* **Data da Coleta/Período dos Dados:** Janeiro de 2014 a Dezembro de 2023
* **Localização Geográfica dos Dados:** Brasil (Sistema Único de Saúde - SUS)
* **Fonte de Financiamento:** Não houve financiamento específico para este estudo.

## COMPARTILHAMENTO E ACESSO

* **Licença do Código:** MIT License (Ver arquivo `LICENSE`)
* **Link para Publicação Associada:** [Inserir Link para o artigo na RESS quando disponível]
* **Localização dos Dados Originais:** Os dados brutos são derivados do Sistema de Informações Hospitalares do Sistema Único de Saúde (SIH/SUS) e podem ser acessados publicamente através do Departamento de Informática do SUS (DATASUS): <http://www2.datasus.gov.br/DATASUS/index.php?area=0202>. O download e pré-processamento inicial podem ser facilitados pelo pacote `microdatasus` [19].
* **Citação Recomendada para este Código/Repositório:**
    Pereira JR, Silva LA, Gomes MM, Clavijo B. (2025). Código de Análise para: Fatores associados à readmissão hospitalar e mortalidade por artrite séptica no Sistema Único de Saúde, Brasil, 2014-2023. [Software]. GitHub Repository. [Inserir URL do Repositório GitHub Aqui].

## VISÃO GERAL DOS DADOS E ARQUIVOS

* **Lista de Arquivos:**
    * `README.md`: Este arquivo de descrição.
    * `analise_artrite_septica_ress.py`: Script Python principal contendo todo o fluxo de análise.
    * `LICENSE`: Arquivo de licença MIT.
    * `requirements.txt`: Lista das bibliotecas Python necessárias e suas versões (aproximadas).
    * `ResultadosAnalise_ArtigoRESS/` (Pasta gerada pelo script): Contém as figuras (.png, .tiff) e tabelas auxiliares (.csv) resultantes da execução do script.
    * **(Opcional)** `SIH_ArtriteSeptica_BrasilUFporUF_filtered61225.csv`: Arquivo de dados de entrada utilizado (NÃO incluído neste repositório devido ao tamanho e por ser derivado de fonte pública. Instruções para obtenção abaixo).
* **Relação entre Arquivos:** O script `analise_artrite_septica_ress.py` lê o arquivo `.csv` (que deve ser obtido separadamente) e gera os conteúdos da pasta `ResultadosAnalise_ArtigoRESS/`.

## INFORMAÇÕES METODOLÓGICAS

* **Método de Coleta/Geração dos Dados:** Os dados são registros administrativos de internações hospitalares (AIHs) do SIH/SUS, coletados rotineiramente pelos serviços de saúde e consolidados pelo DATASUS. A seleção inicial de casos baseou-se nos códigos CID-10 M00.0-M00.9 (Pioartrites). Um filtro inicial para idade >= 18 anos e limpeza de dados inconsistentes foi aplicado para gerar o arquivo de entrada `SIH_ArtriteSeptica_BrasilUFporUF_filtered61225.csv`. **Instruções detalhadas para obter e processar dados brutos do DATASUS podem ser encontradas na documentação do pacote `microdatasus` ([https://github.com/rfsaldanha/microdatasus](https://github.com/rfsaldanha/microdatasus)) [19]**.
* **Método de Processamento (Script):** O script `analise_artrite_septica_ress.py` realiza as seguintes etapas:
    1.  Carregamento e limpeza adicional dos dados.
    2.  Análise descritiva da coorte.
    3.  Identificação de readmissões em 30 dias usando um identificador proxy (MUNIC\_RES + NASC + SEXO + CEP) e análise temporal das internações.
    4.  Categorização operacional dos procedimentos registrados (`PROC_NOME`) em 5 níveis com base em palavras-chave.
    5.  Geração de gráficos (Mortalidade x Idade, Readmissão x Procedimento).
    6.  Transformação de variáveis (Z-score para Idade, Logaritmo natural para Tempo de Permanência).
    7.  Ajuste de modelo de regressão logística multivariada para identificar fatores associados à readmissão.
    8.  Geração de Forest Plot para os resultados da regressão.
    9.  Salvamento dos resultados tabulares e gráficos.
* **Software e Bibliotecas:**
    * Python (versão 3.9 ou superior recomendada)
    * Bibliotecas (ver `requirements.txt`): pandas, numpy, matplotlib, seaborn, statsmodels, scikit-learn.
* **Procedimentos de Garantia de Qualidade:** O código foi desenvolvido com base nas análises exploratórias e modelos gerados via JuliusAI, com validação cruzada dos resultados principais (descritivos, taxas, ORs) em relação aos reportados no manuscrito final. A lógica de identificação de readmissão e categorização de procedimentos foi reconstruída e comentada para transparência. Recomenda-se a execução do script para verificar a reprodutibilidade dos resultados.
* **Pessoas Envolvidas:** Análise e interpretação dos dados: JRP, MMG, BC. Desenvolvimento e validação do código final: JRP (com auxílio de ferramentas de IA e revisão por MMG, BC).

## INFORMAÇÕES ESPECÍFICAS DO ARQUIVO DE DADOS (PARA `SIH_ArtriteSeptica_BrasilUFporUF_filtered61225.csv`)

* **Número de Variáveis:** (Número original de colunas no arquivo SIH/SUS processado)
* **Número de Casos/Linhas:** 61.225 (após filtros iniciais)
* **Lista de Variáveis Principais Utilizadas no Script:**
    * `munic_res`: Código do município de residência (usado no proxy ID).
    * `nasc`: Data de nascimento (usado no proxy ID).
    * `sexo`: Sexo do paciente (1=Masculino, 2=Feminino; usado no proxy ID e análise).
    * `cep`: Código de Endereçamento Postal (usado no proxy ID).
    * `dt_inter`: Data de internação (YYYYMMDD ou YYYY-MM-DD).
    * `dt_saida`: Data de saída (YYYYMMDD ou YYYY-MM-DD).
    * `dias_perm`: Dias de permanência na internação índice.
    * `idade`: Idade do paciente em anos na internação.
    * `morte`: Indicador de óbito hospitalar (1=Sim, 0=Não).
    * `proc_rea`/`proc_nome`: Código/Nome do procedimento principal realizado (base para categorização).
    * `ident_proxy`: Identificador proxy criado para rastrear readmissões.
    * `readmitido_30d`: Flag indicando readmissão em 30 dias (1=Sim, 0=Não).
    * `PROC_CATEGORIA`: Categoria operacional do procedimento (5 níveis).
    * `IDADE_padronizada`: Idade transformada em Z-score.
    * `DIAS_PERM_log`: Dias de permanência transformados por logaritmo natural.
* **Códigos de Dados Faltantes:** Tratados como NaN pelo `pandas` durante a leitura ou conversão. Registros com NaNs em colunas essenciais foram removidos.
* **Abreviações:**
    * SIH/SUS: Sistema de Informações Hospitalares do Sistema Único de Saúde
    * CID-10: Classificação Internacional de Doenças, 10ª Revisão
    * SIGTAP: Tabela de Procedimentos, Medicamentos e OPM do SUS
    * OR: Odds Ratio
    * IC95%: Intervalo de Confiança de 95%
    * DP: Desvio Padrão
    * IIQ: Intervalo Interquartil
    * AIH: Autorização de Internação Hospitalar

## COMO EXECUTAR O CÓDIGO

1.  **Clone o repositório:**
    ```bash
    git clone [https://docs.github.com/articles/referencing-and-citing-content](https://docs.github.com/articles/referencing-and-citing-content)
    cd [nome-do-repositorio]
    ```
2.  **Obtenha os Dados:** Baixe os microdados relevantes do SIH/SUS via DATASUS (<http://www2.datasus.gov.br/DATASUS/index.php?area=0202>) para o período 2014-2023. Aplique os filtros iniciais (CID-10 M00.0-M00.9, idade >= 18, limpeza básica) para gerar o arquivo `SIH_ArtriteSeptica_BrasilUFporUF_filtered61225.csv` e coloque-o na mesma pasta do script. (Alternativamente, use o pacote `microdatasus` para auxiliar neste processo).
3.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Execute o script:**
    ```bash
    python analise_artrite_septica_ress.py
    ```
5.  **Verifique os resultados:** Os arquivos de saída (figuras e tabelas CSV) serão salvos na pasta `ResultadosAnalise_ArtigoRESS/`.

---
*(Fim do README.md)*
