# 🛒 Amazon Titles Fine-Tuning

Amazon Titles Fine-Tuning é um projeto que utiliza o dataset [The AmazonTitles-1.3MM](https://github.com/amazon-science/amazon-titles-1.3m), composto por consultas textuais reais de usuários e títulos de produtos relevantes da Amazon, acompanhados de suas descrições. O objetivo do projeto é aplicar técnicas de fine-tuning em modelos de linguagem (LLM), com foco em Llama 3, para melhorar o entendimento e a geração de títulos para produtos, otimizando a experiência de busca e recomendação.

---

## 🗂️ Sumário

- [📚 Sobre o Projeto](#sobre-o-projeto)
- [🗄️ Dataset](#dataset)
- [⚡ Pipeline de Treinamento](#pipeline-de-treinamento)
- [🛠️ Instalação](#instalação)
- [📁 Estrutura do Projeto](#estrutura-do-projeto)
- [🤝 Contribuição](#contribuição)
- [📝 Licença](#licença)

---

## 📚 Sobre o Projeto

Este projeto busca aprimorar modelos de NLP para tarefas relacionadas à geração e compreensão de títulos de produtos a partir de consultas de usuários, utilizando dados reais extraídos da Amazon. O fine-tuning permite adaptar modelos pré-treinados para tarefas específicas, aumentando a precisão e relevância dos resultados apresentados aos usuários.

O pipeline é totalmente compatível com Google Colab, aproveitando recursos como armazenamento em Google Drive e publicação automática na HuggingFace Hub.

---

## 🗄️ Dataset

- **Nome:** The AmazonTitles-1.3MM
- **Descrição:** Contém consultas de busca, títulos de produtos e descrições.
- **Fonte:** [Amazon Science - Dataset](https://github.com/amazon-science/amazon-titles-1.3m)
- **Formato:** Arquivos CSV/TSV com mais de 1.3 milhão de exemplos.
- **Dataset customizado:** Este projeto utiliza uma versão pré-processada chamada `"guillherms/amazon_titles_alpaca_cleaned_v2"` hospedada no HuggingFace.

---

## ⚡ Pipeline de Treinamento

O notebook principal realiza as seguintes etapas:

1. **Instalação de dependências**  
   Instala as bibliotecas Unsloth, xformers, peft, accelerate, bitsandbytes, evaluate, datasets e rouge-score.

2. **Montagem do Google Drive**  
   Permite salvar checkpoints e snapshots de forma persistente.

3. **Carregamento do modelo Llama 3.2-3B em modo 4-bit**  
   Utiliza Unsloth para otimização de memória e performance.

4. **Configuração do Fine-Tuning via LoRA**  
   Adapta os módulos de atenção e feedforward do modelo usando técnicas eficientes de fine-tuning.

5. **Pré-processamento do dataset**  
   Converte dados para formato ShareGPT, aplica templates de chat e divide em blocos de 10k exemplos para treino incremental.

6. **Treinamento incremental e gerenciamento de checkpoints**  
   Cada bloco é treinado individualmente, salvando checkpoints e snapshots ao final de cada etapa.

7. **Avaliação automática**  
   Mede o desempenho do modelo usando métricas ROUGE-L e BLEU a cada bloco.

8. **Publicação na HuggingFace Hub**  
   Após o treinamento, o modelo e as métricas são enviados automaticamente para o repositório público.

---

## 🛠️ Instalação

1. Clone o repositório:
   ```bash
   git clone https://github.com/guillherms/amazon-titles-finetune.git
   cd amazon-titles-finetune
   ```

2. (Opcional) Execute o notebook principal no Google Colab para aproveitar todos os recursos automáticos do pipeline.

---

## 📁 Estrutura do Projeto

```
amazon-titles-finetune/
├── notebooks/                            # Jupyter Notebooks para fine-tuning, avaliação e publicação
│   └── fine_tunned_llama_3_2_3b.ipynb    # Pipeline principal
└── README.md                             # Este arquivo
```

---

**Autor:** [guillherms](https://github.com/guillherms)

---

## ✨ Exemplos de Resultados

- Métricas de cada bloco de treino são salvas em CSV e disponíveis no [repositório HuggingFace](https://huggingface.co/guillherms/llama-3.2-3b-amazon-titles-100k-lora).
- Modelo treinado disponível para inferência ou continuação do fine-tuning.

---