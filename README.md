# 🏘️ Economia de Trocas dos Aldeões (Villagers) — Minecraft

Projeto de análise de dados que simula, em Python, a mecânica de **demanda** do Minecraft (o preço de um trade sobe a cada compra repetida) e explora os resultados em um **dashboard interativo no Power BI**. O projeto foi feito pra experimentar análise de dados aplicando à um interesse pessoal, bem como o uso da IA como ferramenta para a coleta de dados, tarefas repetitivas, estruturação de documentos formais e como ferramenta de ensino.

## 🎯 Objetivo

Entender, com dados reais das tabelas de comércio da [Minecraft Wiki](https://minecraft.wiki), como o preço de uma negociação evolui conforme o jogador compra repetidamente o mesmo item, e comparar esse comportamento entre as 13 profissões de aldeão e seus 5 níveis de especialização (Novice → Master).

## 🧮 Metodologia

1. Foram reunidas **185 negociações reais** (preço-base, multiplicador de preço e limite de usos) das 13 profissões de aldeão.
2. Cada negociação foi simulada compra a compra, do primeiro até o último uso permitido (`max_trades`), aplicando a fórmula oficial do jogo:

   ```
   aumento = int(price_multiplier × demand × base_price)
   preço_pago = base_price + aumento
   ```

   onde `demand` começa em 0 e sobe 1 a cada compra realizada.
3. O resultado (**2.319 linhas**, uma por compra simulada) foi exportado para `villager_economy.csv`.
4. O CSV foi carregado no Power BI para construir o dashboard `VillagerReport.pbix`.

## 📁 Estrutura do repositório

| Arquivo | Descrição |
|---|---|
| `villagerdata.py` | Script Python que define os trades e roda a simulação (`simulate_price`), gerando o `villager_economy.csv` |
| `villager_economy.csv` | Base de dados simulada (2.319 linhas) usada no Power BI |
| `VillagerReport.pbix` | Arquivo do dashboard no Power BI |
| `VillagerReport.pdf` | Exportação do dashboard em PDF |
| `Relatorio_Economia_Villagers.docx` | Relatório escrito com a análise dos gráficos e dos dados |

## 📊 O dashboard

O dashboard traz, por profissão: preço médio, preço máximo e total de compras simuladas (KPIs), além de gráficos de aumento médio de preço, preço médio por item, preço por número de compras (curva de demanda) e preço médio por nível de profissão.

## 🔎 Principais achados

- O preço sobe de forma **linear e previsível** a cada compra — não há aleatoriedade na mecânica de demanda.
- **Librarian** tem o maior preço médio (24,77) das 13 profissões, mas isso é puxado quase sozinho pelo *Enchanted Book* (35 esmeraldas, multiplicador 0,2), que se repete em todos os 5 níveis dessa profissão.
- Apenas 45 das 185 negociações usam o multiplicador de preço mais agressivo (0,2); são elas — como *Bell* e *Enchanted Book* — que disparam no gráfico de preço por número de compras.
- Contraintuitivamente, o nível **Novice** tem preço médio maior (16,49) que o **Master** (7,61): trades de nível Master costumam ter `max_trades = 3`, travando o preço logo nas primeiras compras, enquanto muitos trades Novice permitem de 12 a 16 usos.

## 🛠️ Tecnologias utilizadas

- **Python** (pandas) — simulação dos dados
- **Power BI** — construção do dashboard
- **Google Colab** — ambiente de desenvolvimento da simulação

## ▶️ Como reproduzir

```bash
pip install pandas
python villagerdata.py
```

Isso gera o `villager_economy.csv`, que pode ser aberto diretamente no Power BI ou importado no `VillagerReport.pbix`.

## ✍️ Autor

**Sabrina A. Modesto** — projeto de aprendizado de análise de dados e Power BI.

