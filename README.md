# Gerador de Leads Fictícios para Brasil

Projeto em Python para gerar dados simulados de leads brasileiros, incluindo CPF válido, telefone regionalizado, endereço, data de nascimento e nome validado. Ideal para testes, demos, ou simplesmente para você convencer seu chefe que já tem "base" suficiente.

## ⚠️ Aviso Legal Importante! ⚠️
Este projeto gera dados inteiramente fictícios, criados aleatoriamente com finalidades exclusivamente educacionais e de teste. 

Nenhum dado aqui foi coletado de indivíduos reais.
Embora o gerador utilize combinações aleatórias, pode haver coincidência involuntária com dados reais (como nomes, CPFs ou endereços). Tal coincidência é puramente acidental e não intencional.

**Nota Legal:** Este projeto é distribuído sob a Licença MIT e não oferece nenhuma garantia. O autor não se responsabiliza por qualquer uso indevido das informações geradas, incluindo, mas não se limitando a, fraudes, estelionato, violação de privacidade ou qualquer outro uso ilegal ou antiético. Use por sua conta e risco.

## Funcionalidades

- Geração de **CPF válido** conforme regra oficial.  
- Telefones com **DDD regionalizado** baseado no estado (incluindo distribuição probabilística de DDDs alternativos).  
- Nomes gerados com o pacote `Faker` para Brasil, com limpeza de títulos (Dr., Prof., Sr., etc).  
- Endereços completos (CEP, logradouro, bairro, cidade, estado) a partir de base real de CEPs do Brasil.  
- Complemento de endereço coerente (casa, apartamento, condomínio).  
- Data de nascimento gerada entre 18 e 73 anos (fixa para a data de 05/08/2025).  
- Exportação dos leads para arquivo CSV com encoding UTF-8.  

---

## Como funciona

1. Carrega arquivos auxiliares:  
   - `cepsbrasil.json`: base de CEPs com ruas e bairros.  
   - `ddds.json`: DDDs regionais por estado e seus DDDs alternativos.

2. Inicializa o Faker com localidade `pt_BR`.  

3. Amostra aleatoriamente 256 CEPs únicos da base.  

4. Para cada amostra:  
   - Gera um nome limpo, sem títulos.  
   - Gera CPF válido.  
   - Gera telefone com DDD regional, misturando DDDs principais e alternativos com probabilidade.  
   - Gera data de nascimento entre 18 e 73 anos.  
   - Monta endereço completo com possibilidade de complemento coerente.  

5. Salva tudo em um CSV `leads_gerados.csv`.  

---

## Dependências

- Python 3.8+  
- Faker (`pip install faker`)  

---

## Estrutura dos arquivos necessários

- `cepsbrasil.json` — JSON com lista de CEPs, cada um com campos:  
  `cep`, `rua`, `bairro`, `cidade`, `estado`  
- `ddds.json` — JSON com mapeamento:  
  ```json
  [
    {
      "uf": "SP",
      "principais": ["11", "12"],
      "alternativos": ["13", "14"]
    },
    ...
  ]

## Exemplo de saída em csv
| id       | nome           | telefone           | nascimento  | cpf         | cep       | uf | logradouro                                             | bairro    | cidade         | complemento           |
|----------|----------------|--------------------|-------------|-------------|-----------|----|--------------------------------------------------------|-----------|----------------|------------------------|
| 0001056  | Vicente Santos | +55 (45) 90808-2056| 1974-04-19  | 73648034596 | 81010270  | PR | Rua Djalma Ferreira Maciel - de 241/242 ao fim         | Lindóia   | Curitiba       | Bloco C1, Apto 641     |
| 0001057  | Dom da Rosa    | +55 (22) 97584-7800| 1968-11-02  | 81346053464 | 25615500  | RJ | Vila Francisco Verrissimo da Silva                     | Quissama  | Petrópolis     | Bloco C2, Apto 880     |


## Como usar

Primeiro será necessário baixar o dataset oficial de ceps, este está no repositório do txt dadoscepsbrasil
depois baixar e salvar no repositório como dadoscepsbrasil.json o resto o código faz por si

Para rodar basta ir no bloco superior em configurações de uso e configurar esses dois parâmetros e rodar do código
#configurações iniciais
num_leads = 256 - Configura a quantidade de leads geradas
id_inicial = 1056 - Configura o id inicial de sistema para não parecer que é algo consolidado

