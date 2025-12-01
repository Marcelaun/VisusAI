## 👁️ VisusAI - Plataforma de Diagnóstico de Retinopatia Diabética

**Link para acessar online a plataforma:** [(https://visus-ai-frontend.vercel.app/)]

**VisusAI** é uma solução SaaS (Software as a Service) completa para auxílio ao diagnóstico de Retinopatia Diabética, conectando médicos, pacientes e Inteligência Artificial em uma plataforma unificada.O projeto foi desenvolvido com foco em uma arquitetura de microsserviços híbrida (Cloud + Edge) para garantir disponibilidade, segurança e baixo custo de infraestrutura.


## 🏗️ Arquitetura do Sistema

O sistema opera de forma distribuída, conectando serviços na nuvem e servidores on-premise (Edge Computing).
```
    User[Médico / Paciente] -->|HTTPS| Frontend[Frontend (React/Vercel)]
    Frontend -->|API REST| Cloudflare[Cloudflare Tunnel]
    Cloudflare -->|HTTP2| Backend[Backend Laravel (Docker @ TV Box/Edge)]
    
    Backend -->|SQL| DB[(Supabase PostgreSQL)]
    Backend -->|Upload/Download| Storage[(Supabase Storage S3)]
    Backend -->|Inferência| AI_Service[Microserviço IA (Python/FastAPI @ HuggingFace)]
    
    AI_Service -->|JSON| Backend
    Backend -->|PDF| Frontend
```

**Componentes Principais**

1. **Frontend (React + Vite):** Interface moderna e responsiva hospedada na Vercel. Gerencia o fluxo de usuários (Médicos e Pacientes) com autenticação via Token e persistência local.Backend
2. **(Laravel 11):** API Gateway hospedada em hardware próprio (TV Box ARM64) containerizada com Docker. Gerencia regras de negócio, filas, autenticação e geração de laudos.
3. **Banco de Dados (Supabase PostgreSQL):** Base de dados relacional na nuvem. Utilizamos o Session Pooler (Porta 5432) para garantir compatibilidade IPv4 com o Docker.
4. **Storage (Supabase S3 Bucket):** Armazenamento de objetos para as imagens de alta resolução dos exames de retina.
5. **Serviço de IA (Python/FastAPI):** API isolada hospedada no Hugging Face Spaces, rodando o modelo EfficientNet-B4 treinado com PyTorch.

## 🛠️ Tecnologias Utilizadas 

**Backend & Infraestrutura**
* **Laravel 11:** Framework PHP robusto para API REST.
* **Docker & Docker Compose:** Containerização otimizada para arquitetura linux/arm64 (TV Box).
* **Nginx:** Servidor Web configurado como Proxy Reverso.
* **Cloudflare Tunnel:** Exposição segura de localhost para a internet (Zero Trust).
* * **Supabase:**
  * **Database:** PostgreSQL gerenciado.
  * **Storage:** Bucket S3 para imagens médicas.
  * **Auth:** (Opcional) Integração preparada para futuro.
**Frontend**
* **React.js:** Biblioteca para construção de interfaces.
* **Material UI (MUI):** Componentes visuais e Skeleton Loading.
* **Axios:** Cliente HTTP com interceptors para Tokens.
* **React Router:** Navegação SPA.
* **React Toastify:** Feedback visual de ações.
**Inteligência Artificial (Data Science)**
* **Modelo:** EfficientNet-B4 (Transfer Learning).
* **Framework:** PyTorch & Timm.
* * **Engenharia de Dados:**
  * **CLAHE:** Pré-processamento para realce de contraste.
  * **WeightedRandomSampler:** Correção de desbalanceamento de classes.
  * **Albumentations:** Data Augmentation avançado.

## 🚀 Funcionalidades

**Para o Médico (Profissional)**
* **Cadastro e Login Seguro:** Autenticação via Token.
* **Gestão de Pacientes: CRUD completo de pacientes.
* **Nova Análise:** Upload de imagens de retina (com suporte a arquivos pesados via Nginx).
* **Resultado IA:** Visualização de heatmap e probabilidades de diagnóstico.
* **Emissão de Laudo:** Editor de texto para parecer médico e geração automática de PDF.
**Para o Paciente**
* **Acesso Simplificado:** Login via CPF e Data de Nascimento (sem senha).
* **Histórico:** Visualização de todos os exames realizados.
* **Download:** Acesso direto ao Laudo PDF validado pelo médico.
**Administrativo**
* **Painel Admin:** Gestão de profissionais e aprovação de novos cadastros.
## 🔧 Como Executar (Localmente)

**Pré-requisitos** 
* **Docker e Docker Compose**
* **Node.js v18+**
* **Conta no Supabase (para DB e Storage)**
* **Conta no Hugging Face (para o modelo)**


## 🧠 Sobre o Modelo de IA
O modelo foi treinado utilizando o dataset **APTOS 2019**, contendo milhares de imagens de retina classificadas em 5 níveis de severidade.
Métrica  Valor 
**Acurácia** 82%
**Kappa Score** 0.90 (Excelente concordância)

**🔗 Links do projeto:**
* [Frontend (React)](https://github.com/Marcelaun/visus-ai-frontend)
* [Backend (Laravel)](https://github.com/Marcelaun/backend_laravel).
* [IA Service (Hugging Face)](https://github.com/Marcelaun/visus-ai-model)

