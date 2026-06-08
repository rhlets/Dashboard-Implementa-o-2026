import { useState, useEffect } from "react";

// ─────────────────────────────────────────────────────────────
// COMPLETE DATA — all fields from spreadsheet
// ─────────────────────────────────────────────────────────────
const QUARTERS = [
  {
    id:"Q1.1", label:"Q1.1", color:"#FF5A1A",
    name:"Fundamentação e Estruturação Básica", period:"Junho – Agosto 2026",
    phases:[
      {
        id:"P01", num:"01", name:"Diagnóstico e Alinhamento Estratégico",
        responsible:"Gestor(a) de RH",
        participants:["Liderança Executiva","Gestores de Tecnologia e CS","Equipe de TI","Colaboradores Chave"],
        marcos:["Compreensão aprofundada da cultura e processos atuais","Benefícios PJ organizados e comunicados","Base documental essencial estabelecida e acessível","Estrutura inicial do RH definida"],
        kpis:["% de gestores entrevistados (meta: 100%)","% de VMMV e Manifesto Cultural aprovados pela liderança (meta: 100%)","% de políticas essenciais criadas e aprovadas (meta: 100%)","Repositório ativo com 100% dos documentos iniciais migrados","Estrutura do RH definida e comunicada internamente","PDI inicial para o RH em andamento"],
        goals:["Concluir o diagnóstico e mapeamento de processos em 100%","Criar e aprovar 3 políticas essenciais","Implementar o repositório de cultura e migrar 100% dos documentos existentes","Definir a estrutura e iniciar o PDI do RH"],
        items:[
          {id:"1.1",name:"Mapeamento de Processos de RH Atuais",wr:"Sem. 1–3",period:"Junho",ws:1,we:3,
            desc:"Entrevistas com gestores, levantamento de processos informais, análise cultural, ferramentas de comunicação.",
            bullets:["Entrevistas aprofundadas com gestores (Tecnologia, CS e outros) para entender desafios, expectativas e percepções sobre gestão de pessoas","Levantamento de processos informais de contratação, desligamento, comunicação e gestão de benefícios","Análise de documentos culturais existentes","Levantamento de ferramentas de comunicação (Slack) e outras tecnologias"]},
          {id:"1.2",name:"Estruturação de Documentos Essenciais",wr:"Sem. 2–5",period:"Jun – Jul",ws:2,we:5,
            desc:"Código de Conduta, Políticas Fundamentais, Repositório Centralizado, Manual de Benefícios PJ.",
            bullets:["Criação do Código de Conduta e Ética da empresa","Elaboração de Políticas Fundamentais: Anticorrupção, Segurança da Informação, Uso de Recursos da Empresa","Desenvolvimento de Guia de Boas Práticas para uso do Slack (etiqueta, canais, performance)","Implementação de Repositório Centralizado de Documentos — seleção e configuração de plataforma (Google Drive, SharePoint, Notion)","Migração dos documentos existentes para o repositório","Levantamento detalhado de todos os benefícios oferecidos aos PJs","Criação do Espaço Cultura LET'S — regras, elegibilidade e como utilizar","Comunicação do Manual de Benefícios aos colaboradores"]},
          {id:"1.3",name:"Estruturação do Setor de RH",wr:"Sem. 2–4",period:"Junho",ws:2,we:4,
            desc:"Estrutura organizacional do RH, competências, base integrada ao Claude, ficha de registro.",
            bullets:["Definição da estrutura organizacional do RH (funções e responsabilidades)","Mapeamento das competências necessárias para o time de RH","Criação da base de gestão de pessoas integrada ao Claude","Melhoria da ficha de registro LET'S"]}
        ]
      },
      {
        id:"P02", num:"02", name:"Onboarding e Integração",
        responsible:"Gestor(a) de RH",
        participants:["Gestores de Tecnologia e CS","Novos Colaboradores","Financeiro"],
        marcos:["Programa de Onboarding estruturado e piloto realizado","Integração entre times iniciada","VMMV formalizados e comunicados"],
        kpis:["% de novos colaboradores que passaram pelo onboarding piloto (meta: 100%)","% de colaboradores que acessaram o Manual de Benefícios","Feedback positivo dos participantes do onboarding piloto","Início de iniciativas de integração entre times"],
        goals:["Desenvolver e testar o programa de onboarding","Iniciar a estrutura de VMMV"],
        items:[
          {id:"2.1",name:"Desenvolvimento do Programa de Onboarding",wr:"Sem. 5–6",period:"Julho",ws:5,we:6,
            desc:"Roteiro de onboarding (pré-boarding → 1º mês), kit de boas-vindas digital.",
            bullets:["Criação de roteiro de onboarding para novos colaboradores (pré-boarding, 1º dia, 1ª semana, 1º mês)","Conteúdo do onboarding: cultura, VMMV, políticas, apresentação da empresa, áreas e ferramentas","Desenvolvimento de kit de boas-vindas digital"]},
          {id:"2.2",name:"Integração entre Times",wr:"Sem. 6–8",period:"Julho",ws:6,we:8,
            desc:"Café com o Líder, Shadowing, projetos interdepartamentais Tecnologia ↔ CS.",
            bullets:["Mapeamento de pontos de contato e dependências entre Tecnologia e CS","Criação de iniciativas de integração: 'Café com o Líder', 'Shadowing' entre áreas","Implementação de projetos interdepartamentais"]},
          {id:"2.3",name:"Formalização de VMMV e Cultura",wr:"Sem. 5–7",period:"Julho",ws:5,we:7,
            desc:"Workshops de co-criação com liderança, Manifesto Cultural.",
            bullets:["Workshops com a liderança para co-criação/validação da Visão, Missão e Valores","Definição de 'quem queremos ser' como cultura","Elaboração de Manifesto Cultural ou Princípios de Cultura"]}
        ]
      },
      {
        id:"P03", num:"03", name:"Base de Gestão de Pessoas e IA",
        responsible:"Gestor(a) de RH",
        participants:["Equipe de TI","Liderança Executiva","Gestores de Tecnologia e CS"],
        marcos:["Base de Gestão de Pessoas implementada","IA integrada na gestão de documentos","Desenho inicial de níveis hierárquicos e autonomia"],
        kpis:["HRIS/Plataforma Cloud implementada com dados de 100% dos colaboradores","Ferramenta de IA para gestão de documentos configurada e em uso pelo RH","Esboço de níveis hierárquicos e autonomia para Tecnologia e CS","Feedback positivo do RH sobre a ferramenta de IA"],
        goals:["Implementar a Base de Gestão de Pessoas (Cloud)","Integrar documentos em nuvem e IA na gestão","Apresentar desenho inicial de níveis hierárquicos e autonomia para validação"],
        items:[
          {id:"3.1",name:"Implementação da Base de Gestão de Pessoas",wr:"Sem. 6–9",period:"Jul – Ago",ws:6,we:9,
            desc:"HRIS / plataforma Cloud, migração de dados, perfis de acesso.",
            bullets:["Seleção e configuração de HRIS (BambooHR, Sólides) ou plataforma Cloud (Notion/Airtable) para centralizar dados de colaboradores PJ","Migração inicial de dados de colaboradores para a plataforma","Definição de perfis de acesso e segurança"]},
          {id:"3.2",name:"Integração de IA na Gestão de Documentos",wr:"Sem. 9–11",period:"Agosto",ws:9,we:11,
            desc:"Categorização automática, busca inteligente, sumarização, treinamento.",
            bullets:["Exploração e implementação de ferramentas de IA para categorização automática de documentos","Busca inteligente por palavras-chave e conteúdo","Sumarização de políticas com IA","Treinamento da equipe de RH para uso das ferramentas"]},
          {id:"3.3",name:"Desenho Inicial de Níveis Hierárquicos e Autonomia",wr:"Sem. 10–12",period:"Agosto",ws:10,we:12,
            desc:"Estrutura de níveis (Júnior → Liderança), indicadores de autonomia.",
            bullets:["Mapeamento das principais funções e responsabilidades","Esboço de estrutura de níveis (Júnior, Pleno, Sênior, Especialista, Liderança) para Tecnologia e CS","Definição de indicadores de autonomia esperada para cada nível"]}
        ]
      }
    ]
  },
  {
    id:"Q1.2", label:"Q1.2", color:"#C026D3",
    name:"Desenvolvimento de Lideranças e Performance", period:"Agosto – Outubro 2026",
    phases:[
      {
        id:"P04", num:"04", name:"Capacitação de Lideranças",
        responsible:"Gestor(a) de RH",
        participants:["Gestores de Tecnologia e CS","Liderança Executiva","Colaboradores"],
        marcos:["Programa de Desenvolvimento de Lideranças (PDL) iniciado","Cultura de feedback contínuo implementada"],
        kpis:["% de gestores nos módulos iniciais do PDL (meta: 80%)","% de colaboradores no treinamento de feedback (meta: 70%)","Taxa de adesão aos 'Check-ins de Feedback' (meta: 60%)","Feedback positivo dos gestores sobre o PDL"],
        goals:["Iniciar o PDL com 2 módulos","Treinar 70% dos colaboradores em feedback","Implementar a ferramenta de registro de feedback"],
        items:[
          {id:"4.1",name:"Lançamento do PDL — Programa de Desenvolvimento de Lideranças",wr:"Sem. 11–13",period:"Agosto",ws:11,we:13,
            desc:"Módulos de liderança essencial, feedback construtivo e alta performance.",
            bullets:["Módulo 'Liderança Essencial': comunicação, delegação, gestão de conflitos","Módulo 'Feedback Construtivo': como dar e receber feedback de forma estruturada","Módulo 'Gestão de Equipes de Alta Performance': metodologias e práticas","Workshops presenciais ou online","Criação de guia para gestores sobre como aplicar os aprendizados"]},
          {id:"4.2",name:"Implementação da Cultura de Feedback",wr:"Sem. 12–13",period:"Agosto",ws:12,we:13,
            desc:"Treinamento para colaboradores, check-ins, ferramenta de registro.",
            bullets:["Treinamento para todos os colaboradores sobre a importância e como dar/receber feedback","Criação de modelo de 'Check-in de Feedback' (mensal ou quinzenal) para gestores e liderados","Ferramenta para registro de feedback (módulo do HRIS ou ferramenta dedicada)"]}
        ]
      },
      {
        id:"P05", num:"05", name:"Gestão de Performance e PDI",
        responsible:"Gestor(a) de RH",
        participants:["Gestores de Tecnologia e CS","Colaboradores","Liderança Executiva"],
        marcos:["Ciclo de Avaliação de Desempenho (gestor-colaborador) concluído","PDIs formalizados e em andamento","Política de Retenção em desenvolvimento"],
        kpis:["% de colaboradores com avaliação concluída (meta: 100%)","% de colaboradores com PDI formalizado (meta: 90%)","Rascunho da Política de Retenção elaborado","Feedback dos colaboradores sobre o processo de avaliação"],
        goals:["Concluir o 1º ciclo de avaliação de desempenho","Garantir que 90% dos colaboradores tenham PDI","Apresentar o rascunho da Política de Retenção para a liderança"],
        items:[
          {id:"5.1",name:"Implementação da Avaliação de Desempenho",wr:"Sem. 14–16",period:"Setembro",ws:14,we:16,
            desc:"Critérios, formulário, treinamento de gestores, 1º ciclo.",
            bullets:["Definição de critérios de avaliação alinhados aos VMMV e objetivos da empresa","Criação de formulário de avaliação (módulo do HRIS ou ferramenta específica)","Treinamento para gestores sobre como realizar a avaliação e dar feedback","Realização do 1º ciclo de avaliação de desempenho (gestor-colaborador)"]},
          {id:"5.2",name:"Formalização de PDIs",wr:"Sem. 16–17",period:"Setembro",ws:16,we:17,
            desc:"PDIs baseados em avaliações e objetivos de carreira, ferramenta de acompanhamento.",
            bullets:["Orientação para gestores e colaboradores na criação de PDIs baseados nos resultados da avaliação","Alinhamento com objetivos de carreira individuais","Ferramenta para acompanhamento dos PDIs (módulo do HRIS)"]},
          {id:"5.3",name:"Desenvolvimento da Política de Retenção",wr:"Sem. 14–16",period:"Setembro",ws:14,we:16,
            desc:"Pesquisa de mercado, brainstorming com liderança, elaboração.",
            bullets:["Pesquisa de mercado sobre práticas de retenção para PJs","Brainstorming com a liderança sobre fatores de retenção (reconhecimento, desenvolvimento, ambiente, benefícios)","Início da elaboração da Política de Retenção"]}
        ]
      },
      {
        id:"P06", num:"06", name:"Estrutura de Cargos e Fluxos",
        responsible:"Gestor(a) de RH",
        participants:["Liderança Executiva","Gestores de Tecnologia e CS","Financeiro","Jurídico","Equipe de TI"],
        marcos:["Estrutura de Cargos e Salários PJ definida","Sistema de Gestão de Contratos implementado","Fluxo de aprovação de cadeiras desenhado e comunicado"],
        kpis:["Estrutura de Cargos e Salários PJ aprovada pela liderança","Sistema de gestão de contratos ativo com 100% dos contratos migrados","Feedback dos gestores sobre a clareza da estrutura de cargos"],
        goals:["Definir e comunicar a Estrutura de Cargos e Salários PJ","Implementar o sistema de gestão de contratos","Desenhar e comunicar o fluxo de aprovação de cadeiras"],
        items:[
          {id:"6.1",name:"Estrutura de Cargos e Salários PJ",wr:"Sem. 15–18",period:"Set – Out",ws:15,we:18,
            desc:"Mapeamento, descrições, benchmarking PJ, grades, análise CLT x PJ.",
            bullets:["Mapeamento detalhado de cargos e funções existentes","Definição de descrições de cargos (responsabilidades, requisitos, competências)","Pesquisa de mercado para benchmarking de remuneração PJ","Criação de tabela de referência de remuneração por nível/cargo/grades","Análise CLT x PJ","Comunicação da estrutura aos gestores"]},
          {id:"6.2",name:"Sistema de Gestão de Contratos PJ",wr:"Sem. 18–20",period:"Outubro",ws:18,we:20,
            desc:"Ferramenta de contratos, migração de contratos existentes, alertas de vencimento.",
            bullets:["Seleção e configuração de ferramenta para controle de contratos PJ (módulo HRIS ou software dedicado)","Migração de todos os contratos existentes para o sistema","Definição de alertas para vencimento de contratos"]},
          {id:"6.3",name:"Fluxo de Aprovação de Cadeiras",wr:"Sem. 19–20",period:"Outubro",ws:19,we:20,
            desc:"Fluxo formal, formulário padronizado, comunicação aos gestores.",
            bullets:["Mapeamento do processo atual de solicitação de novas posições","Fluxo formal: Requisição do Gestor → Análise RH → Aprovação Financeira → Aprovação da Liderança Executiva","Criação de formulário padronizado para solicitação de cadeiras","Comunicação do fluxo e formulário aos gestores"]}
        ]
      }
    ]
  },
  {
    id:"T1.1", label:"T1.1", color:"#7C3AED",
    name:"Cultura de Desenvolvimento e Engajamento", period:"Outubro – Novembro 2026",
    phases:[
      {
        id:"P07", num:"07", name:"Avaliação 360° e Desenvolvimento Contínuo",
        responsible:"Gestor(a) de RH",
        participants:["Gestores de Tecnologia e CS","Colaboradores","Liderança Executiva"],
        marcos:["Ciclo de Avaliação 360° concluído","Programas de desenvolvimento contínuo em andamento"],
        kpis:["% de colaboradores que participaram da Avaliação 360° (meta: 80%)","% de colaboradores com plano de ação pós-360°","% de participação nos workshops/treinamentos","Feedback positivo sobre a relevância dos programas"],
        goals:["Concluir o 1º ciclo de Avaliação 360°","Lançar 2 programas de desenvolvimento contínuo","Criar a biblioteca de recursos de aprendizagem"],
        items:[
          {id:"7.1",name:"Implementação da Avaliação 360°",wr:"Sem. 19–21",period:"Outubro",ws:19,we:21,
            desc:"Competências avaliadas, ferramenta, treinamento, 1º ciclo, devolutivas.",
            bullets:["Definição de competências a serem avaliadas (alinhadas aos VMMV e descrições de cargo)","Seleção de ferramenta para Avaliação 360° (módulo HRIS ou ferramenta dedicada)","Treinamento para gestores e colaboradores sobre o processo e a importância do feedback 360°","Realização do 1º ciclo de Avaliação 360°","Sessões de devolutiva e apoio na interpretação dos resultados"]},
          {id:"7.2",name:"Programas de Desenvolvimento Contínuo",wr:"Sem. 20–22",period:"Out – Nov",ws:20,we:22,
            desc:"Workshops, mentoria interna/coaching, biblioteca de recursos.",
            bullets:["Oferta de workshops e treinamentos específicos baseados nas lacunas identificadas nas avaliações e PDIs","Lançamento de programas de mentoria interna (gestores experientes mentorando colaboradores) ou coaching","Criação de biblioteca de recursos de aprendizagem (cursos online, artigos, livros)"]}
        ]
      },
      {
        id:"P08", num:"08", name:"Gestão de Talentos e Desligamento",
        responsible:"Gestor(a) de RH",
        participants:["Liderança Executiva","Gestores de Tecnologia e CS","Jurídico","Financeiro"],
        marcos:["Política de Desligamento estruturada e comunicada","Mapeamento de Talentos e Sucessão iniciado","Fluxo de aprovação de desligamento desenhado e comunicado"],
        kpis:["Política de Desligamento aprovada e comunicada","% de gestores treinados em desligamento","Mapeamento de talentos chave iniciado","Fluxo de aprovação de desligamento documentado e comunicado","Taxa de preenchimento de entrevistas de saída (meta: 80%)"],
        goals:["Formalizar e comunicar a Política de Desligamento","Iniciar o mapeamento de talentos e sucessão","Desenhar e comunicar o fluxo de aprovação de desligamento"],
        items:[
          {id:"8.1",name:"Política de Desligamento",wr:"Sem. 22–23",period:"Novembro",ws:22,we:23,
            desc:"Política humanizada, treinamento de gestores, entrevista de saída.",
            bullets:["Elaboração de política de desligamento humanizada e transparente (processo, comunicação, feedback, documentação)","Treinamento para gestores sobre como conduzir um desligamento","Criação de formulário de entrevista de desligamento para coletar feedback","Comunicação da política aos gestores"]},
          {id:"8.2",name:"Mapeamento de Talentos e Sucessão",wr:"Sem. 23–25",period:"Novembro",ws:23,we:25,
            desc:"Posições críticas, Nine Box Grid, planejamento de sucessão.",
            bullets:["Identificação de posições críticas e talentos chave na empresa","Criação de 'Nine Box Grid' ou ferramenta similar para avaliar potencial e performance","Início do planejamento de sucessão para posições estratégicas"]},
          {id:"8.3",name:"Fluxo de Aprovação de Desligamento",wr:"Sem. 22–24",period:"Novembro",ws:22,we:24,
            desc:"Fluxo: Gestor → RH → Liderança → Jurídico → Financeiro.",
            bullets:["Mapeamento do processo atual de desligamento","Fluxo formal: Solicitação do Gestor → Análise RH (motivo, impacto) → Aprovação da Liderança → Aprovação Jurídica (conformidade) → Aprovação Financeira","Criação de formulário padronizado para solicitação de desligamento","Comunicação do fluxo e formulário aos gestores"]}
        ]
      },
      {
        id:"P09", num:"09", name:"Clima e Comunicação Interna",
        responsible:"Gestor(a) de RH",
        participants:["Liderança Executiva","Gestores de Tecnologia e CS","Colaboradores","Equipe de Marketing/Comunicação"],
        marcos:["Pesquisa de Clima Organizacional realizada","Plano de Ação pós-pesquisa em andamento","Canais de comunicação interna fortalecidos"],
        kpis:["% de participação na pesquisa de clima (meta: 80%)","Plano de ação de clima elaborado e comunicado","% de ações do plano de clima iniciadas","Feedback positivo sobre a transparência dos resultados","Ferramenta de IA para análise de sentimento em teste"],
        goals:["Realizar a pesquisa de clima com 80% de participação","Elaborar e comunicar o plano de ação de clima","Lançar a newsletter interna","Iniciar a integração de IA na comunicação interna"],
        items:[
          {id:"9.1",name:"Pesquisa de Clima Organizacional",wr:"Sem. 22–24",period:"Novembro",ws:22,we:24,
            desc:"Ferramenta, perguntas sobre engajamento e liderança, coleta e análise.",
            bullets:["Seleção de ferramenta para pesquisa de clima (SurveyMonkey, Typeform ou ferramenta especializada)","Definição de perguntas e temas: engajamento, liderança, cultura, ambiente de trabalho, benefícios","Lançamento e coleta de dados da pesquisa","Análise dos resultados e elaboração de relatório"]},
          {id:"9.2",name:"Plano de Ação Pós-Pesquisa de Clima",wr:"Sem. 24–25",period:"Novembro",ws:24,we:25,
            desc:"Apresentação dos resultados, plano de ação, grupos de trabalho.",
            bullets:["Apresentação dos resultados à liderança e aos colaboradores (transparência)","Criação de plano de ação com iniciativas para abordar os pontos de melhoria identificados","Formação de grupos de trabalho para implementar as ações"]},
          {id:"9.3",name:"Fortalecimento da Comunicação Interna",wr:"Sem. 23–25",period:"Novembro",ws:23,we:25,
            desc:"Calendário editorial, Newsletter Interna, IA para análise de sentimento.",
            bullets:["Avaliação dos canais de comunicação existentes (Slack, e-mail, reuniões)","Criação de calendário editorial de comunicação interna","Lançamento de Newsletter Interna ou canal de notícias regular","Exploração de ferramentas de IA para análise de sentimento no Slack e otimização de mensagens"]}
        ]
      }
    ]
  },
  {
    id:"T1.2", label:"T1.2", color:"#0D9488",
    name:"Otimização, Inovação e Sustentabilidade", period:"Dezembro 2026",
    phases:[
      {
        id:"P10", num:"10", name:"Otimização de Processos e IA",
        responsible:"Gestor(a) de RH",
        participants:["Equipe de TI","Gestores de Tecnologia e CS","Liderança Executiva"],
        marcos:["Processos de RH otimizados e automatizados","IA integrada em Recrutamento e Seleção (R&S)","Centralização de informações aprimorada com IA"],
        kpis:["% de processos de RH com automação implementada (meta: 30%)","Ferramenta de IA para R&S em uso","Funcionalidades avançadas de IA no repositório ativas","Redução do tempo médio de triagem de currículos","Feedback positivo do RH sobre eficiência das automações"],
        goals:["Automatizar 30% dos processos de RH","Implementar IA em R&S","Aprimorar a centralização de informações com IA"],
        items:[
          {id:"10.1",name:"Otimização e Automação de Processos de RH",wr:"Sem. 26–27",period:"Dezembro",ws:26,we:27,
            desc:"Revisão de processos, gargalos, automações de workflows e integrações.",
            bullets:["Revisão de todos os processos de RH implementados (onboarding, avaliação, desligamento, etc.)","Identificação de gargalos e oportunidades de automação","Implementação de automações: e-mails automáticos, workflows e integração entre sistemas"]},
          {id:"10.2",name:"Integração de IA em Recrutamento e Seleção",wr:"Sem. 26–27",period:"Dezembro",ws:26,we:27,
            desc:"Triagem de currículos, análise de perfis, chatbots para candidatos.",
            bullets:["Exploração e implementação de ferramentas de IA para triagem de currículos (análise de palavras-chave e competências)","Análise de perfil de candidatos com IA","Chatbots para pré-entrevistas e FAQ de candidatos","Treinamento para o RH no uso das ferramentas"]},
          {id:"10.3",name:"Centralização de Informações com IA Avançada",wr:"Sem. 26–28",period:"Dezembro",ws:26,we:28,
            desc:"Busca semântica, sumarização automática, relatórios com IA.",
            bullets:["Aprimoramento do repositório Cloud com busca semântica avançada","Sumarização automática de documentos longos com IA","Geração de relatórios e insights a partir de dados não estruturados"]}
        ]
      },
      {
        id:"P11", num:"11", name:"Avaliação de Liderança e Reconhecimento",
        responsible:"Gestor(a) de RH",
        participants:["Liderança Executiva","Gestores de Tecnologia e CS","Colaboradores","Financeiro"],
        marcos:["Política de Avaliação do Gestor implementada"],
        kpis:["% de gestores avaliados pelos colaboradores (meta: 90%)"],
        goals:["Implementar a Política de Avaliação do Gestor"],
        items:[
          {id:"11.1",name:"Política de Avaliação do Gestor pelos Colaboradores",wr:"Sem. 26–27",period:"Dezembro",ws:26,we:27,
            desc:"Critérios, ferramenta, 1º ciclo de avaliação, sessões de devolutiva.",
            bullets:["Definição de critérios para avaliação dos gestores pelos colaboradores (liderança, comunicação, desenvolvimento da equipe, feedback)","Seleção de ferramenta para a avaliação (módulo do HRIS ou ferramenta dedicada)","Lançamento do 1º ciclo de avaliação dos gestores","Sessões de devolutiva para os gestores e planos de desenvolvimento"]}
        ]
      },
      {
        id:"P12", num:"12", name:"Planejamento Estratégico e Sustentabilidade",
        responsible:"Gestor(a) de RH",
        participants:["Liderança Executiva","Gestores de Tecnologia e CS","Equipe de TI","Financeiro"],
        marcos:["Planejamento Estratégico de RH para o próximo ano","Relatório de Indicadores de RH consolidado","Base de Gestão de Pessoas completa e funcional"],
        kpis:["Plano Estratégico de RH para o próximo ano aprovado","Dashboard de KPIs de RH atualizado e apresentado mensalmente","HRIS/Plataforma Cloud com 100% dos dados e funcionalidades ativas","Feedback positivo da liderança sobre a contribuição estratégica do RH"],
        goals:["Apresentar o Plano Estratégico de RH para o próximo ano","Consolidar e apresentar o dashboard de KPIs de RH","Garantir a plena funcionalidade da Base de Gestão de Pessoas (Cloud)"],
        items:[
          {id:"12.1",name:"Planejamento Estratégico de RH Anual",wr:"Sem. 28",period:"Dezembro",ws:28,we:28,
            desc:"Revisão dos resultados, objetivos, metas e orçamento para o próximo ciclo.",
            bullets:["Revisão dos resultados do ano","Definição de objetivos e metas de RH para o próximo ciclo, alinhados aos objetivos de negócio","Orçamento de RH para o próximo ano"]},
          {id:"12.2",name:"Dashboard de Indicadores de RH (KPIs)",wr:"Sem. 28",period:"Dezembro",ws:28,we:28,
            desc:"Dashboard completo no HRIS/Power BI, apresentação à liderança.",
            bullets:["Criação de dashboard completo de KPIs de RH (utilizando HRIS, Power BI ou outra ferramenta)","Apresentação regular dos resultados à liderança executiva"]},
          {id:"12.3",name:"Base de Gestão de Pessoas (Cloud) Completa",wr:"Sem. 28",period:"Dezembro",ws:28,we:28,
            desc:"HRIS totalmente funcional, dados migrados, processos integrados, IA otimizada.",
            bullets:["Garantir que o HRIS/plataforma Cloud esteja totalmente funcional","100% dos dados migrados, processos integrados e IA otimizada","Documentação completa de todos os processos e sistemas de RH"]}
        ]
      }
    ]
  }
];

// ─── constants ───────────────────────────────────────────────
const STORAGE_KEY = "lets-rh-impl-2026-v2";
const ST = {
  pending:     { label:"Pendente",      color:"#B45309", bg:"#FFFBEB", ring:"#FDE68A", dot:"#F59E0B" },
  in_progress: { label:"Em Andamento",  color:"#C2410C", bg:"#FFF7ED", ring:"#FDBA74", dot:"#FF5A1A" },
  done:        { label:"Concluído",     color:"#065F46", bg:"#ECFDF5", ring:"#6EE7B7", dot:"#059669" },
};
const ST_ORDER = ["pending","in_progress","done"];
const getSt   = (sts,id) => sts[id]?.status || "pending";
const getDate = (sts,id) => sts[id]?.completedAt || "";
const allItems = () => QUARTERS.flatMap(q=>q.phases.flatMap(p=>p.items));

// ─── helpers ─────────────────────────────────────────────────
function ProgressBar({value,color,height=6,bg="#E5EAF2"}){
  return(
    <div style={{background:bg,borderRadius:99,height,overflow:"hidden"}}>
      <div style={{height:"100%",borderRadius:99,width:`${value}%`,background:color,transition:"width .4s ease"}}/>
    </div>
  );
}

function Chip({label,color,bg,border}){
  return(
    <span style={{display:"inline-flex",alignItems:"center",fontSize:11,fontWeight:600,
      color,background:bg,border:`1px solid ${border||color+"40"}`,borderRadius:20,
      padding:"3px 10px",letterSpacing:"0.03em",lineHeight:1,whiteSpace:"nowrap"}}>
      {label}
    </span>
  );
}

function StatusBtn({status,onClick}){
  const s=ST[status];
  return(
    <button onClick={onClick} style={{display:"inline-flex",alignItems:"center",gap:5,
      padding:"4px 11px",borderRadius:20,border:`1px solid ${s.ring}`,
      background:s.bg,color:s.color,fontSize:11,fontWeight:600,cursor:"pointer",
      fontFamily:"inherit",letterSpacing:"0.03em",whiteSpace:"nowrap",
      transition:"all .15s",lineHeight:1}}>
      <span style={{width:6,height:6,borderRadius:"50%",background:s.dot,flexShrink:0}}/>
      {s.label}
    </button>
  );
}

// ─── STAT CARD ───────────────────────────────────────────────
function StatCard({label,value,color,sub}){
  return(
    <div style={{background:"#FFF",border:"1px solid #E5EAF2",borderRadius:14,padding:"20px 22px",
      boxShadow:"0 1px 4px rgba(0,0,0,.04)",borderTop:`3px solid ${color}`}}>
      <div style={{fontSize:11,fontWeight:700,color:"#9DAFBF",letterSpacing:"0.06em",textTransform:"uppercase",marginBottom:6}}>{label}</div>
      <div style={{fontSize:36,fontWeight:800,color,lineHeight:1,marginBottom:4}}>{value}</div>
      {sub&&<div style={{fontSize:12,color:"#9DAFBF"}}>{sub}</div>}
    </div>
  );
}

// ─── QUARTER PROGRESS CARD ───────────────────────────────────
function QCard({q,sts}){
  const all=q.phases.flatMap(p=>p.items);
  const done=all.filter(i=>getSt(sts,i.id)==="done").length;
  const ip=all.filter(i=>getSt(sts,i.id)==="in_progress").length;
  const pct=Math.round((done/all.length)*100);
  return(
    <div style={{background:"#FFF",border:"1px solid #E5EAF2",borderRadius:14,padding:"20px 22px",
      boxShadow:"0 1px 4px rgba(0,0,0,.04)",borderLeft:`4px solid ${q.color}`}}>
      <div style={{display:"flex",justifyContent:"space-between",alignItems:"flex-start",marginBottom:12}}>
        <div>
          <div style={{marginBottom:6}}><Chip label={q.label} color={q.color} bg={q.color+"15"} border={q.color+"40"}/></div>
          <div style={{fontSize:13,fontWeight:600,color:"#1E293B",lineHeight:1.4,maxWidth:260}}>{q.name}</div>
          <div style={{fontSize:11,color:"#94A3B8",marginTop:3}}>{q.period}</div>
        </div>
        <div style={{textAlign:"right",flexShrink:0}}>
          <div style={{fontSize:30,fontWeight:800,color:q.color,lineHeight:1}}>{pct}%</div>
          <div style={{fontSize:11,color:"#94A3B8"}}>{done}/{all.length} entregas</div>
        </div>
      </div>
      <ProgressBar value={pct} color={q.color} height={6}/>
      <div style={{display:"flex",gap:14,marginTop:8,flexWrap:"wrap"}}>
        {ip>0&&<span style={{fontSize:11,color:q.color,fontWeight:500}}>● {ip} em andamento</span>}
        {(all.length-done-ip)>0&&<span style={{fontSize:11,color:"#94A3B8"}}>● {all.length-done-ip} pendente{all.length-done-ip!==1?"s":""}</span>}
        {done===all.length&&<span style={{fontSize:11,color:"#059669",fontWeight:500}}>✓ Todas concluídas</span>}
      </div>
    </div>
  );
}

// ─── DASHBOARD VIEW ──────────────────────────────────────────
function DashboardView({sts}){
  const all=allItems();
  const done=all.filter(i=>getSt(sts,i.id)==="done").length;
  const ip=all.filter(i=>getSt(sts,i.id)==="in_progress").length;
  const pending=all.length-done-ip;
  const pct=Math.round((done/all.length)*100);
  const upcoming=all.filter(i=>getSt(sts,i.id)!=="done").sort((a,b)=>a.ws-b.ws).slice(0,6);
  return(
    <div style={{display:"flex",flexDirection:"column",gap:24}}>
      <div style={{display:"grid",gridTemplateColumns:"repeat(4,1fr)",gap:14}}>
        <StatCard label="Total de Entregas" value={all.length} color="#3B82F6" sub="micro-entregas mapeadas"/>
        <StatCard label="Concluídas" value={done} color="#059669" sub={`${pct}% do total`}/>
        <StatCard label="Em Andamento" value={ip} color="#FF5A1A" sub="em execução agora"/>
        <StatCard label="Pendentes" value={pending} color="#D97706" sub="aguardando início"/>
      </div>
      <div style={{background:"#FFF",border:"1px solid #E5EAF2",borderRadius:14,padding:"22px 24px",boxShadow:"0 1px 4px rgba(0,0,0,.04)"}}>
        <div style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:14}}>
          <div>
            <div style={{fontSize:13,fontWeight:700,color:"#1E293B"}}>Progresso Geral — Implementação RH 2026</div>
            <div style={{fontSize:12,color:"#94A3B8",marginTop:2}}>Semanas 1–28 · Junho a Dezembro de 2026</div>
          </div>
          <div style={{fontSize:38,fontWeight:800,color:"#FF5A1A"}}>{pct}<span style={{fontSize:16,color:"#CBD5E1"}}>%</span></div>
        </div>
        <ProgressBar value={pct} color="#FF5A1A" height={10}/>
        <div style={{display:"flex",gap:20,marginTop:12,flexWrap:"wrap"}}>
          {[["#059669","Concluído",done],["#FF5A1A","Em Andamento",ip],["#D97706","Pendente",pending]].map(([c,l,v])=>(
            <div key={l} style={{display:"flex",alignItems:"center",gap:6}}>
              <span style={{width:8,height:8,borderRadius:"50%",background:c,flexShrink:0}}/>
              <span style={{fontSize:12,color:"#64748B"}}>{l}: <strong style={{color:"#1E293B"}}>{v}</strong></span>
            </div>
          ))}
        </div>
      </div>
      <div>
        <div style={{fontSize:11,fontWeight:700,color:"#94A3B8",letterSpacing:"0.06em",textTransform:"uppercase",marginBottom:12}}>Progresso por Trimestre</div>
        <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:14}}>
          {QUARTERS.map(q=><QCard key={q.id} q={q} sts={sts}/>)}
        </div>
      </div>
      {upcoming.length>0&&(
        <div>
          <div style={{fontSize:11,fontWeight:700,color:"#94A3B8",letterSpacing:"0.06em",textTransform:"uppercase",marginBottom:12}}>Próximas Entregas</div>
          <div style={{background:"#FFF",border:"1px solid #E5EAF2",borderRadius:14,overflow:"hidden",boxShadow:"0 1px 4px rgba(0,0,0,.04)"}}>
            {upcoming.map((item,i)=>{
              const qd=QUARTERS.find(q=>q.phases.some(p=>p.items.includes(item)));
              const s=ST[getSt(sts,item.id)];
              return(
                <div key={item.id} style={{display:"flex",alignItems:"center",gap:12,padding:"13px 20px",
                  borderBottom:i<upcoming.length-1?"1px solid #F1F5F9":"none"}}>
                  <Chip label={qd.label} color={qd.color} bg={qd.color+"12"} border={qd.color+"35"}/>
                  <span style={{flex:1,fontSize:13,color:"#334155",overflow:"hidden",textOverflow:"ellipsis",whiteSpace:"nowrap"}}>{item.name}</span>
                  <span style={{fontSize:11,color:"#94A3B8",whiteSpace:"nowrap"}}>{item.wr}</span>
                  <span style={{fontSize:10,fontWeight:600,color:s.color,background:s.bg,border:`1px solid ${s.ring}`,borderRadius:20,padding:"2px 9px"}}>{s.label}</span>
                </div>
              );
            })}
          </div>
        </div>
      )}
    </div>
  );
}

// ─── TASK ROW ─────────────────────────────────────────────────
function TaskRow({item,qColor,sts,cycleStatus,setDate}){
  const st=getSt(sts,item.id);
  const dt=getDate(sts,item.id);
  const s=ST[st];
  const [open,setOpen]=useState(false);
  return(
    <div style={{borderBottom:"1px solid #F1F5F9",background:st==="done"?"#F7FDF9":"transparent",transition:"background .2s"}}>
      <div style={{display:"flex",alignItems:"center",gap:10,padding:"12px 18px",flexWrap:"wrap"}}>
        <span style={{fontSize:10,fontWeight:700,color:qColor,background:qColor+"12",
          border:`1px solid ${qColor}35`,borderRadius:20,padding:"2px 9px",flexShrink:0}}>{item.id}</span>
        <div style={{flex:1,minWidth:160}}>
          <span onClick={()=>setOpen(v=>!v)} style={{fontSize:13,color:st==="done"?"#94A3B8":"#1E293B",
            cursor:"pointer",textDecoration:st==="done"?"line-through":"none",lineHeight:1.4}}>{item.name}</span>
        </div>
        <span style={{fontSize:11,color:"#64748B",background:"#F8FAFC",border:"1px solid #E5EAF2",
          borderRadius:8,padding:"3px 9px",whiteSpace:"nowrap",flexShrink:0}}>{item.wr} · {item.period}</span>
        <StatusBtn status={st} onClick={()=>cycleStatus(item.id)}/>
        <input type="date" value={dt} onChange={e=>setDate(item.id,e.target.value)}
          style={{background:"#F8FAFC",border:`1px solid ${dt?s.ring:"#E5EAF2"}`,borderRadius:8,
            color:dt?s.color:"#94A3B8",fontSize:11,padding:"4px 9px",fontFamily:"inherit",
            cursor:"pointer",outline:"none",flexShrink:0}} title="Data de conclusão"/>
      </div>
      {open&&(
        <div style={{padding:"0 18px 14px 18px",paddingLeft:52}}>
          <div style={{fontSize:12,color:"#475569",lineHeight:1.7,background:"#F8FAFC",
            borderRadius:8,padding:"10px 14px",border:"1px solid #E5EAF2"}}>{item.desc}</div>
        </div>
      )}
    </div>
  );
}

// ─── PHASE ACCORDION (tasks) ──────────────────────────────────
function PhaseAccordion({phase,qColor,sts,cycleStatus,setDate}){
  const [open,setOpen]=useState(true);
  const all=phase.items;
  const done=all.filter(i=>getSt(sts,i.id)==="done").length;
  const pct=Math.round((done/all.length)*100);
  return(
    <div style={{marginBottom:10,background:"#FFF",border:"1px solid #E5EAF2",borderRadius:14,overflow:"hidden",boxShadow:"0 1px 3px rgba(0,0,0,.03)"}}>
      <div onClick={()=>setOpen(v=>!v)} style={{display:"flex",alignItems:"center",gap:12,padding:"13px 18px",
        cursor:"pointer",background:open?"#FAFBFC":"#FFF",borderBottom:open?"1px solid #F1F5F9":"none",transition:"background .15s"}}>
        <span style={{width:28,height:28,borderRadius:8,background:qColor+"15",border:`1px solid ${qColor}40`,
          color:qColor,fontSize:11,fontWeight:700,display:"flex",alignItems:"center",justifyContent:"center",flexShrink:0}}>{phase.num}</span>
        <span style={{flex:1,fontSize:14,fontWeight:600,color:"#1E293B"}}>{phase.name}</span>
        <span style={{fontSize:11,color:"#94A3B8"}}>{done}/{all.length}</span>
        <div style={{width:72}}><ProgressBar value={pct} color={qColor} height={4}/></div>
        <span style={{color:"#94A3B8",transform:open?"rotate(90deg)":"rotate(0deg)",transition:"transform .2s",fontSize:14,lineHeight:1}}>›</span>
      </div>
      {open&&all.map(item=><TaskRow key={item.id} item={item} qColor={qColor} sts={sts} cycleStatus={cycleStatus} setDate={setDate}/>)}
    </div>
  );
}

// ─── TASKS VIEW ───────────────────────────────────────────────
function TasksView({sts,cycleStatus,setDate}){
  const [qf,setQf]=useState("all");
  const [sf,setSf]=useState("all");
  const [q,setQ]=useState("");
  const filtered=QUARTERS.filter(x=>qf==="all"||x.id===qf).map(x=>({
    ...x,phases:x.phases.map(p=>({...p,items:p.items.filter(i=>{
      if(sf!=="all"&&getSt(sts,i.id)!==sf)return false;
      if(q&&!i.name.toLowerCase().includes(q.toLowerCase()))return false;
      return true;
    })})).filter(p=>p.items.length>0)
  })).filter(x=>x.phases.length>0);
  const count=filtered.reduce((s,x)=>s+x.phases.reduce((ss,p)=>ss+p.items.length,0),0);
  const SS={background:"#FFF",border:"1px solid #E5EAF2",borderRadius:8,color:"#475569",fontSize:12,
    padding:"8px 12px",fontFamily:"inherit",outline:"none",cursor:"pointer",boxShadow:"0 1px 2px rgba(0,0,0,.03)"};
  return(
    <div style={{display:"flex",flexDirection:"column",gap:20}}>
      <div style={{display:"flex",gap:10,flexWrap:"wrap",alignItems:"center"}}>
        <input type="text" placeholder="🔍  Buscar entregável..." value={q} onChange={e=>setQ(e.target.value)}
          style={{...SS,flex:"1 1 200px",minWidth:180}}/>
        <select value={qf} onChange={e=>setQf(e.target.value)} style={SS}>
          <option value="all">Todos os trimestres</option>
          {QUARTERS.map(x=><option key={x.id} value={x.id}>{x.label} — {x.name}</option>)}
        </select>
        <select value={sf} onChange={e=>setSf(e.target.value)} style={SS}>
          <option value="all">Todos os status</option>
          {Object.entries(ST).map(([k,v])=><option key={k} value={k}>{v.label}</option>)}
        </select>
        <span style={{fontSize:12,color:"#94A3B8",whiteSpace:"nowrap"}}>{count} entrega{count!==1?"s":""}</span>
      </div>
      <div style={{fontSize:11,color:"#94A3B8",background:"#F8FAFC",border:"1px solid #E5EAF2",borderRadius:8,padding:"8px 14px"}}>
        💡 Clique no nome da entrega para ver a descrição · Clique no badge de status para alterar · Preencha a data de conclusão ao finalizar
      </div>
      {filtered.map(x=>(
        <div key={x.id}>
          <div style={{display:"flex",alignItems:"center",gap:10,marginBottom:10}}>
            <Chip label={x.label} color={x.color} bg={x.color+"12"} border={x.color+"40"}/>
            <span style={{fontSize:13,fontWeight:600,color:"#334155"}}>{x.name}</span>
            <span style={{fontSize:11,color:"#94A3B8"}}>· {x.period}</span>
          </div>
          {x.phases.map(p=><PhaseAccordion key={p.id} phase={p} qColor={x.color} sts={sts} cycleStatus={cycleStatus} setDate={setDate}/>)}
        </div>
      ))}
      {filtered.length===0&&<div style={{textAlign:"center",color:"#94A3B8",padding:"60px 20px"}}>Nenhum resultado encontrado.</div>}
    </div>
  );
}

// ─── DETAILS VIEW ─────────────────────────────────────────────
function DetailsView(){
  const [openPhases,setOpenPhases]=useState({});
  const toggle=id=>setOpenPhases(v=>({...v,[id]:!v[id]}));
  const [qf,setQf]=useState("all");
  const visQ=QUARTERS.filter(x=>qf==="all"||x.id===qf);

  const SEC=({title,icon,children})=>(
    <div style={{marginBottom:14}}>
      <div style={{fontSize:11,fontWeight:700,color:"#94A3B8",letterSpacing:"0.06em",textTransform:"uppercase",
        marginBottom:8,display:"flex",alignItems:"center",gap:6}}>
        <span>{icon}</span>{title}
      </div>
      {children}
    </div>
  );

  const BulletList=({items,color})=>(
    <ul style={{margin:0,padding:0,listStyle:"none",display:"flex",flexDirection:"column",gap:5}}>
      {items.map((item,i)=>(
        <li key={i} style={{display:"flex",alignItems:"flex-start",gap:8,fontSize:13,color:"#334155",lineHeight:1.5}}>
          <span style={{color,fontSize:10,marginTop:4,flexShrink:0}}>●</span>
          {item}
        </li>
      ))}
    </ul>
  );

  const SS={background:"#FFF",border:"1px solid #E5EAF2",borderRadius:8,color:"#475569",fontSize:12,
    padding:"8px 12px",fontFamily:"inherit",outline:"none",cursor:"pointer",boxShadow:"0 1px 2px rgba(0,0,0,.03)"};

  return(
    <div style={{display:"flex",flexDirection:"column",gap:24}}>
      <div style={{display:"flex",gap:10,alignItems:"center"}}>
        <select value={qf} onChange={e=>setQf(e.target.value)} style={SS}>
          <option value="all">Todos os trimestres</option>
          {QUARTERS.map(x=><option key={x.id} value={x.id}>{x.label} — {x.name}</option>)}
        </select>
        <span style={{fontSize:12,color:"#94A3B8"}}>Visão completa — todos os campos da planilha</span>
      </div>

      {visQ.map(q=>(
        <div key={q.id}>
          <div style={{display:"flex",alignItems:"center",gap:12,marginBottom:14,padding:"16px 20px",
            background:"#FFF",border:"1px solid #E5EAF2",borderRadius:14,borderLeft:`4px solid ${q.color}`,
            boxShadow:"0 1px 3px rgba(0,0,0,.04)"}}>
            <Chip label={q.label} color={q.color} bg={q.color+"12"} border={q.color+"40"}/>
            <div>
              <div style={{fontSize:15,fontWeight:700,color:"#0F172A"}}>{q.name}</div>
              <div style={{fontSize:12,color:"#94A3B8"}}>{q.period}</div>
            </div>
          </div>

          {q.phases.map(p=>{
            const isOpen=openPhases[p.id]!==false; // default open
            return(
              <div key={p.id} style={{marginBottom:10,background:"#FFF",border:"1px solid #E5EAF2",
                borderRadius:14,overflow:"hidden",boxShadow:"0 1px 3px rgba(0,0,0,.03)"}}>
                {/* Phase header */}
                <div onClick={()=>toggle(p.id)} style={{display:"flex",alignItems:"center",gap:12,
                  padding:"14px 20px",cursor:"pointer",background:isOpen?"#FAFBFC":"#FFF",
                  borderBottom:isOpen?"1px solid #F1F5F9":"none"}}>
                  <span style={{width:30,height:30,borderRadius:8,background:q.color+"15",
                    border:`1px solid ${q.color}40`,color:q.color,fontSize:12,fontWeight:700,
                    display:"flex",alignItems:"center",justifyContent:"center",flexShrink:0}}>{p.num}</span>
                  <span style={{flex:1,fontSize:15,fontWeight:700,color:"#0F172A"}}>{p.name}</span>
                  <span style={{color:"#94A3B8",transform:isOpen?"rotate(90deg)":"rotate(0deg)",
                    transition:"transform .2s",fontSize:16,lineHeight:1}}>›</span>
                </div>

                {isOpen&&(
                  <div style={{padding:"20px 24px",display:"flex",flexDirection:"column",gap:20}}>
                    {/* Marcos */}
                    <SEC title="Marcos Finais do Trimestre" icon="🏁">
                      <BulletList items={p.marcos} color={q.color}/>
                    </SEC>

                    {/* Responsável + Participantes */}
                    <div style={{display:"grid",gridTemplateColumns:"1fr 2fr",gap:14}}>
                      <div style={{background:"#F8FAFC",border:"1px solid #E5EAF2",borderRadius:10,padding:"14px 16px"}}>
                        <div style={{fontSize:11,fontWeight:700,color:"#94A3B8",letterSpacing:"0.06em",textTransform:"uppercase",marginBottom:8}}>👤 Responsável</div>
                        <div style={{fontSize:13,fontWeight:600,color:"#334155"}}>{p.responsible}</div>
                      </div>
                      <div style={{background:"#F8FAFC",border:"1px solid #E5EAF2",borderRadius:10,padding:"14px 16px"}}>
                        <div style={{fontSize:11,fontWeight:700,color:"#94A3B8",letterSpacing:"0.06em",textTransform:"uppercase",marginBottom:8}}>👥 Participantes Chave</div>
                        <div style={{display:"flex",flexWrap:"wrap",gap:6}}>
                          {p.participants.map(x=>(
                            <span key={x} style={{fontSize:12,color:"#475569",background:"#FFF",
                              border:"1px solid #E5EAF2",borderRadius:20,padding:"2px 10px"}}>{x}</span>
                          ))}
                        </div>
                      </div>
                    </div>

                    {/* Entregáveis Detalhados */}
                    <SEC title="Entregáveis Detalhados" icon="📋">
                      <div style={{display:"flex",flexDirection:"column",gap:10}}>
                        {p.items.map(item=>(
                          <div key={item.id} style={{background:"#F8FAFC",border:"1px solid #E5EAF2",
                            borderRadius:10,padding:"14px 16px",borderLeft:`3px solid ${q.color}`}}>
                            <div style={{display:"flex",alignItems:"center",gap:8,marginBottom:10}}>
                              <Chip label={item.id} color={q.color} bg={q.color+"12"} border={q.color+"35"}/>
                              <span style={{fontSize:13,fontWeight:700,color:"#1E293B"}}>{item.name}</span>
                              <span style={{marginLeft:"auto",fontSize:11,color:"#64748B",background:"#FFF",
                                border:"1px solid #E5EAF2",borderRadius:8,padding:"2px 8px",whiteSpace:"nowrap",flexShrink:0}}>
                                {item.wr} · {item.period}
                              </span>
                            </div>
                            <ul style={{margin:0,padding:0,listStyle:"none",display:"flex",flexDirection:"column",gap:4}}>
                              {item.bullets.map((b,i)=>(
                                <li key={i} style={{display:"flex",alignItems:"flex-start",gap:8,fontSize:12,color:"#475569",lineHeight:1.5}}>
                                  <span style={{color:q.color,fontSize:9,marginTop:4.5,flexShrink:0}}>◆</span>{b}
                                </li>
                              ))}
                            </ul>
                          </div>
                        ))}
                      </div>
                    </SEC>

                    {/* KPIs */}
                    <SEC title="Indicadores de Sucesso (KPIs)" icon="📊">
                      <div style={{display:"grid",gridTemplateColumns:"repeat(auto-fill,minmax(260px,1fr))",gap:8}}>
                        {p.kpis.map((k,i)=>(
                          <div key={i} style={{background:"#F8FAFC",border:"1px solid #E5EAF2",borderRadius:8,
                            padding:"10px 12px",display:"flex",alignItems:"flex-start",gap:8}}>
                            <span style={{color:"#3B82F6",fontSize:9,marginTop:4,flexShrink:0}}>◆</span>
                            <span style={{fontSize:12,color:"#334155",lineHeight:1.4}}>{k}</span>
                          </div>
                        ))}
                      </div>
                    </SEC>

                    {/* Goals */}
                    <SEC title="Metas do RH para o Trimestre" icon="🎯">
                      <div style={{display:"flex",flexDirection:"column",gap:6}}>
                        {p.goals.map((g,i)=>(
                          <div key={i} style={{display:"flex",alignItems:"flex-start",gap:10,padding:"10px 14px",
                            background:q.color+"08",border:`1px solid ${q.color}25`,borderRadius:8}}>
                            <span style={{color:q.color,fontWeight:700,fontSize:12,flexShrink:0}}>{i+1}.</span>
                            <span style={{fontSize:13,color:"#334155",lineHeight:1.4}}>{g}</span>
                          </div>
                        ))}
                      </div>
                    </SEC>
                  </div>
                )}
              </div>
            );
          })}
        </div>
      ))}
    </div>
  );
}

// ─── TIMELINE VIEW ────────────────────────────────────────────
function TimelineView({sts}){
  const W=28;
  const MONTHS=[
    {label:"Junho",ws:[1,2,3,4]},{label:"Julho",ws:[5,6,7,8]},
    {label:"Agosto",ws:[9,10,11,12]},{label:"Setembro",ws:[13,14,15,16]},
    {label:"Outubro",ws:[17,18,19,20]},{label:"Novembro",ws:[21,22,23,24,25]},
    {label:"Dezembro",ws:[26,27,28]}
  ];
  const COL=100/W;
  return(
    <div style={{overflowX:"auto"}}>
      <div style={{minWidth:900}}>
        <div style={{display:"flex",marginBottom:4,paddingLeft:220}}>
          {MONTHS.map(m=>(
            <div key={m.label} style={{width:`${m.ws.length*COL}%`,fontSize:10,fontWeight:700,
              color:"#64748B",textTransform:"uppercase",letterSpacing:"0.07em",
              borderLeft:"1px solid #E5EAF2",paddingLeft:6}}>{m.label}</div>
          ))}
        </div>
        <div style={{display:"flex",marginBottom:14,paddingLeft:220}}>
          {Array.from({length:W},(_,i)=>i+1).map(w=>(
            <div key={w} style={{width:`${COL}%`,textAlign:"center",fontSize:9,color:"#CBD5E1",
              borderLeft:"1px solid #F1F5F9"}}>{w}</div>
          ))}
        </div>
        {QUARTERS.map(q=>(
          <div key={q.id} style={{marginBottom:18}}>
            <div style={{display:"flex",alignItems:"center",marginBottom:6}}>
              <div style={{width:220,paddingRight:12,flexShrink:0}}>
                <Chip label={`${q.label} — ${q.name.split(" ").slice(0,3).join(" ")}…`} color={q.color} bg={q.color+"10"} border={q.color+"30"}/>
              </div>
              <div style={{flex:1,height:1,background:q.color+"25"}}/>
            </div>
            {q.phases.map(p=>(
              <div key={p.id} style={{marginBottom:2}}>
                <div style={{display:"flex",alignItems:"flex-start",marginBottom:2}}>
                  <div style={{width:220,flexShrink:0,paddingRight:12,paddingLeft:12}}>
                    <span style={{fontSize:11,color:"#64748B",display:"block",lineHeight:1.3}}>
                      {p.num}. {p.name.split(" ").slice(0,4).join(" ")}
                    </span>
                  </div>
                </div>
                {p.items.map(item=>{
                  const st=getSt(sts,item.id);
                  const s=ST[st];
                  const L=((item.ws-1)/W)*100;
                  const Ww=((item.we-item.ws+1)/W)*100;
                  return(
                    <div key={item.id} style={{display:"flex",alignItems:"center",height:24,marginBottom:2}}>
                      <div style={{width:220,flexShrink:0,paddingRight:12,paddingLeft:24}}>
                        <span style={{fontSize:10,color:st==="done"?"#94A3B8":"#475569",
                          textDecoration:st==="done"?"line-through":"none",
                          display:"block",overflow:"hidden",textOverflow:"ellipsis",whiteSpace:"nowrap"}}>
                          {item.id} {item.name}
                        </span>
                      </div>
                      <div style={{flex:1,position:"relative",height:"100%"}}>
                        {Array.from({length:W},(_,i)=>(
                          <div key={i} style={{position:"absolute",left:`${(i/W)*100}%`,
                            top:0,bottom:0,width:1,background:"#F1F5F9"}}/>
                        ))}
                        <div style={{position:"absolute",left:`${L}%`,width:`${Ww}%`,
                          top:"12%",height:"76%",background:st==="done"?s.dot:q.color,
                          opacity:st==="done"?0.35:0.75,borderRadius:3,transition:"opacity .2s"}}
                          title={`${item.id}: ${item.name} · ${item.wr} · ${s.label}`}/>
                      </div>
                    </div>
                  );
                })}
              </div>
            ))}
          </div>
        ))}
        <div style={{display:"flex",gap:20,marginTop:12,paddingLeft:220,flexWrap:"wrap"}}>
          {Object.entries(ST).map(([k,v])=>(
            <div key={k} style={{display:"flex",alignItems:"center",gap:6}}>
              <span style={{width:22,height:7,borderRadius:3,background:v.dot,opacity:k==="done"?0.35:0.75,flexShrink:0}}/>
              <span style={{fontSize:11,color:"#64748B"}}>{v.label}</span>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
}

// ─── MAIN ─────────────────────────────────────────────────────
export default function HRDashboard(){
  const [tab,setTab]=useState("dashboard");
  const [sts,setSts]=useState({});
  const [loading,setLoading]=useState(true);

  useEffect(()=>{
    (async()=>{
      try{ const r=await window.storage.get(STORAGE_KEY); if(r)setSts(JSON.parse(r.value)); }catch{}
      setLoading(false);
    })();
  },[]);

  const persist=async d=>{ try{await window.storage.set(STORAGE_KEY,JSON.stringify(d));}catch{} };

  const cycleStatus=async id=>{
    const cur=getSt(sts,id);
    const nxt=ST_ORDER[(ST_ORDER.indexOf(cur)+1)%ST_ORDER.length];
    const completedAt=nxt==="done"?new Date().toISOString().split("T")[0]:nxt==="pending"?null:getDate(sts,id);
    const upd={...sts,[id]:{status:nxt,completedAt}};
    setSts(upd); await persist(upd);
  };
  const setDate=async(id,date)=>{
    const upd={...sts,[id]:{...(sts[id]||{status:"pending"}),completedAt:date}};
    setSts(upd); await persist(upd);
  };

  if(loading) return(
    <div style={{display:"flex",alignItems:"center",justifyContent:"center",
      height:"100vh",background:"#F4F7FB",fontFamily:"Plus Jakarta Sans,sans-serif",color:"#FF5A1A",fontSize:16}}>
      Carregando…
    </div>
  );

  const all=allItems();
  const done=all.filter(i=>getSt(sts,i.id)==="done").length;
  const ip=all.filter(i=>getSt(sts,i.id)==="in_progress").length;
  const pct=Math.round((done/all.length)*100);

  const TABS=[
    {id:"dashboard",label:"Visão Geral"},
    {id:"tasks",label:"Tarefas"},
    {id:"details",label:"Detalhes Completos"},
    {id:"timeline",label:"Linha do Tempo"},
  ];

  return(
    <>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap');
        *{box-sizing:border-box;}
        body{margin:0;padding:0;background:#F4F7FB;}
        ::-webkit-scrollbar{width:6px;height:6px;}
        ::-webkit-scrollbar-track{background:#F4F7FB;}
        ::-webkit-scrollbar-thumb{background:#D1D9E6;border-radius:99px;}
        ::-webkit-scrollbar-thumb:hover{background:#B0BCCE;}
        input[type="date"]::-webkit-calendar-picker-indicator{opacity:.5;cursor:pointer;}
        select option{background:#FFF;color:#1E293B;}
        button:hover{filter:brightness(.95);}
      `}</style>

      <div style={{fontFamily:"Plus Jakarta Sans,sans-serif",background:"#F4F7FB",minHeight:"100vh",display:"flex",flexDirection:"column",color:"#1E293B"}}>

        {/* HEADER */}
        <header style={{background:"#FFF",borderBottom:"1px solid #E5EAF2",padding:"14px 28px",
          display:"flex",alignItems:"center",gap:20,flexShrink:0,
          boxShadow:"0 1px 4px rgba(0,0,0,.05)"}}>
          <div style={{display:"flex",alignItems:"center",gap:10}}>
            <div style={{width:38,height:38,borderRadius:10,background:"#FF5A1A",display:"flex",
              alignItems:"center",justifyContent:"center",fontSize:14,fontWeight:900,color:"#FFF"}}>L</div>
            <div>
              <div style={{fontSize:16,fontWeight:800,color:"#0F172A",lineHeight:1,letterSpacing:"-0.3px"}}>
                LET<span style={{color:"#FF5A1A"}}>'S</span> <span style={{color:"#94A3B8",fontWeight:500}}>· RH</span>
              </div>
              <div style={{fontSize:10,color:"#CBD5E1",letterSpacing:"0.07em",fontWeight:600}}>IMPLEMENTAÇÃO 2026</div>
            </div>
          </div>
          <div style={{width:1,height:36,background:"#E5EAF2"}}/>
          <div style={{display:"flex",gap:22,flex:1}}>
            {[["#3B82F6","Total",all.length],["#059669","Concluídas",done],["#FF5A1A","Em Andamento",ip],["#D97706","Pendentes",all.length-done-ip]].map(([c,l,v])=>(
              <div key={l} style={{display:"flex",alignItems:"center",gap:6}}>
                <span style={{fontSize:20,fontWeight:800,color:c,lineHeight:1}}>{v}</span>
                <span style={{fontSize:11,color:"#94A3B8",lineHeight:1.2}}>{l}</span>
              </div>
            ))}
          </div>
          <div style={{display:"flex",alignItems:"center",gap:10,flexShrink:0}}>
            <div style={{textAlign:"right"}}>
              <div style={{fontSize:10,color:"#94A3B8",fontWeight:600}}>PROGRESSO</div>
              <div style={{fontSize:22,fontWeight:800,color:"#FF5A1A",lineHeight:1}}>{pct}%</div>
            </div>
            <div style={{width:100}}><ProgressBar value={pct} color="#FF5A1A" height={8}/></div>
          </div>
        </header>

        {/* TABS */}
        <nav style={{background:"#FFF",borderBottom:"1px solid #E5EAF2",padding:"0 28px",display:"flex",gap:2,flexShrink:0}}>
          {TABS.map(t=>(
            <button key={t.id} onClick={()=>setTab(t.id)} style={{padding:"12px 18px",background:"none",border:"none",
              borderBottom:`2px solid ${tab===t.id?"#FF5A1A":"transparent"}`,
              color:tab===t.id?"#FF5A1A":"#64748B",fontFamily:"inherit",fontSize:13,fontWeight:600,
              cursor:"pointer",transition:"all .15s",letterSpacing:"0.01em"}}>{t.label}</button>
          ))}
        </nav>

        {/* CONTENT */}
        <main style={{flex:1,overflow:"auto",padding:24}}>
          {tab==="dashboard"&&<DashboardView sts={sts}/>}
          {tab==="tasks"&&<TasksView sts={sts} cycleStatus={cycleStatus} setDate={setDate}/>}
          {tab==="details"&&<DetailsView/>}
          {tab==="timeline"&&<TimelineView sts={sts}/>}
        </main>
      </div>
    </>
  );
}
