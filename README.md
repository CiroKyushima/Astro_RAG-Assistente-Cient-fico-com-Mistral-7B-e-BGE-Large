# Astro-RAG: Assistente Científico com Mistral-7B e BGE-Large
Este projeto implementa um pipeline de RAG (Retrieval-Augmented Generation) de alta performance, projetado para extrair e sintetizar informações de uma base de dados local de aproximadamente 1.000 artigos científicos do repositório arXiv (focado em astrofísica e física teórica).

O sistema utiliza modelos de estado da arte para garantir que as respostas sejam tecnicamente precisas e diretamente fundamentadas em evidências bibliográficas.

# Funcionalidades Principais
Ingestão Automatizada: Download e processamento de centenas de PDFs científicos via API do arXiv.

Busca Semântica Avançada: Utilização do modelo BGE-Large-en-v1.5 (top-tier no ranking MTEB) para criar embeddings de 1024 dimensões.

Banco Vetorial: Indexação eficiente com FAISS (Facebook AI Similarity Search) para recuperação em milissegundos.

LLM Quantizado: Implementação do Mistral-7B-Instruct-v0.3 com quantização 4-bit (NF4), permitindo a execução em GPUs de consumo (6GB+ VRAM).

Métricas de Validação: Sistema robusto de verificação de qualidade para mitigar alucinações.

# Stack Tecnológica
LLM: Mistral-7B-Instruct-v0.3 (via Hugging Face transformers).

Embeddings: BAAI/bge-large-en-v1.5.

Processamento de PDF: PyPDF2 e Regex para limpeza de texto acadêmico.

Banco de Vetores: FAISS.

Hardware Optimization: BitsAndBytes (quantização), PyTorch (CUDA).

# Avaliação de Qualidade (Framework de Métricas)
O diferencial deste projeto é a inclusão de um relatório de verificação científica após cada resposta:

Fidelidade Semântica: Mede a aderência da resposta aos documentos recuperados (Cosine Similarity).

Gap Analysis (Alucinação Negativa): Verifica se o modelo trouxe informações novas dos artigos ou apenas parafraseou a pergunta.

Densidade de Informação: Avalia a riqueza lexical e precisão técnica do texto gerado.

Performance do Retriever: Analisa a relevância dos trechos encontrados pelo modelo de busca.

# Como funciona o fluxo?
Busca: O código varre o arXiv por temas específicos (ex: cat:astro-ph).

Fragmentação: Textos são divididos em chunks de 512 tokens com sobreposição (overlap) para manter o contexto.

Indexação: Os vetores são armazenados no FAISS.

Prompt: Ao receber uma pergunta, o sistema recupera os top-K trechos e os injeta em um prompt sistêmico rigoroso.

Geração: O Mistral gera a análise baseando-se unicamente nas referências fornecidas.

Próximos Passos
[ ] Implementar uma interface gráfica com Streamlit.

[ ] Adicionar suporte a múltiplos idiomas.

[ ] Integrar técnicas de Re-ranking para melhorar a precisão da busca.
