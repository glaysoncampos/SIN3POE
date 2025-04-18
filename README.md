CRIE UM : Aplicativo de Simulação de Internação IPASGO Saúde (Java Treinamentos)

1. Introdução

Este documento detalha os requisitos para o desenvolvimento de um aplicativo web de simulação de faturamento de internações hospitalares de curta duração (até 4 dias) para o Instituto de Assistência dos Servidores Públicos do Estado de Goiás (IPASGO Saúde). Este simulador, a ser desenvolvido pela Java Treinamentos utilizando a tecnologia Next.js, será uma ferramenta educacional de acesso público ("DeepSite") com o objetivo de familiarizar usuários com o processo de faturamento hospitalar no contexto do IPASGO Saúde. As informações contidas neste documento são baseadas na análise detalhada do processo de faturamento descrita no documento "Simulação de Internação. D.1 (1).pdf".

2. Objetivos do Projeto

O principal objetivo deste projeto é desenvolver uma aplicação educacional móvel acessível via web (dado o uso de Next.js e o acesso público "DeepSite") que simule o processo de faturamento de contas de internação hospitalar de curta duração (até 4 dias) junto ao IPASGO Saúde. A finalidade é oferecer uma ferramenta prática e precisa para alunos que estão iniciando na área de faturamento hospitalar em Goiás e nunca tiveram experiência prévia. O simulador também poderá ser útil para outros profissionais e interessados em compreender o processo.

3. Público-Alvo

O público-alvo principal deste aplicativo de simulação é composto por:

Alunos e estudantes da área de saúde e faturamento hospitalar em Goiás.
4. Escopo do Projeto

O aplicativo de simulação abrangerá o processo de faturamento de internações hospitalares de curta duração (até 4 dias) junto ao IPASGO Saúde, focando nos seguintes aspectos, conforme detalhado no documento base:

Cálculo da permanência (número de diárias).
Valoração das diárias hospitalares de diferentes tipos de acomodação, com base na Tabela de Serviços Hospitalares do IPASGO Saúde.
Valoração das taxas hospitalares (sala cirúrgica, uso de equipamentos, etc.), com base na Tabela de Serviços Hospitalares do IPASGO Saúde.
Valoração de procedimentos médicos realizados durante a internação, utilizando códigos TUSS e informações da Tabela Médica do IPASGO Saúde, incluindo valores de insumos, auxiliares e anestesia quando aplicável.
Valoração de materiais e medicamentos utilizados durante a internação, utilizando códigos TUSS/IPASGO e preços da Tabela de Materiais e Medicamentos do IPASGO Saúde, considerando a necessidade de autorização prévia.
Apresentação de um resumo da conta simulada, detalhando os custos por categoria (diárias, taxas, procedimentos, materiais, medicamentos) e o valor total.
Indicação de potenciais glosas na simulação devido à falta de autorização prévia (simulada).
O simulador não incluirá o faturamento de honorários médicos, que são geralmente faturados separadamente. Esta distinção será claramente comunicada ao usuário.

5. Requisitos Funcionais

O aplicativo deverá permitir aos usuários:

Inserir dados básicos da internação:
Datas e horários de admissão e alta do paciente.
Tipo de acomodação utilizada (enfermaria, apartamento, UTI, etc.).
Diagnóstico principal (opcionalmente com código CID-10).
Selecionar procedimentos médicos realizados:
Apresentar uma lista de procedimentos médicos baseada em um subconjunto representativo de códigos TUSS da Tabela Médica do IPASGO Saúde.
Para cada procedimento, permitir indicar se houve anestesia e o porte anestésico (se aplicável).
Permitir indicar o número de auxiliares (se aplicável).
Considerar se o procedimento possui insumos associados conforme a Tabela Médica.
Selecionar materiais utilizados:
Apresentar uma lista de materiais baseada em um subconjunto representativo de códigos TUSS/IPASGO da Tabela de Materiais e Medicamentos do IPASGO Saúde.
Para cada material, permitir inserir a quantidade utilizada.
Permitir simular o status da autorização prévia (autorizado/não autorizado) para materiais que a requerem.
Selecionar medicamentos administrados:
Apresentar uma lista de medicamentos baseada em um subconjunto representativo de códigos TUSS/IPASGO da Tabela de Materiais e Medicamentos do IPASGO Saúde.
Para cada medicamento, permitir inserir a quantidade/dose administrada.
Permitir simular o status da autorização prévia (autorizado/não autorizado) para medicamentos que a requerem.
Informar sobre visitas médicas:
Permitir inserir o número de visitas médicas diárias (utilizando o código TUSS 10102019 ou código IPASGO 00020010 como referência). O escopo da inclusão destas no cálculo da conta hospitalar será um parâmetro a ser definido (ver item 6.1.7).
Calcular a permanência:
Calcular automaticamente o número de diárias de internação com base nas datas e horários de admissão e alta.
Implementar uma regra de cálculo de diárias configurável pelo usuário ou adotar uma premissa de mercado comum (com clara explicação da regra utilizada) para lidar com o dia da alta e internações com menos de 24 horas.
Calcular o custo da internação:
Calcular o custo das diárias multiplicando o número de diárias pela tarifa correspondente ao tipo de acomodação, buscando os valores na Tabela de Serviços Hospitalares do IPASGO Saúde.
Calcular o custo das taxas hospitalares aplicáveis (sala cirúrgica, equipamentos, etc.), buscando os valores na Tabela de Serviços Hospitalares do IPASGO Saúde e considerando as seleções de procedimentos (porte anestésico).
Calcular o custo dos procedimentos médicos, buscando os valores base e adicionais (anestesia, auxiliares, insumos) na Tabela Médica do IPASGO Saúde para os códigos selecionados.
Calcular o custo dos materiais utilizados, multiplicando a quantidade pelo preço unitário da Tabela de Materiais e Medicamentos do IPASGO Saúde, considerando o status de autorização simulado. Materiais não autorizados (simulados) devem ser indicados como potenciais glosas ou excluídos do cálculo final (a ser definido).
Calcular o custo dos medicamentos administrados, multiplicando a quantidade/dose pelo preço unitário da Tabela de Materiais e Medicamentos do IPASGO Saúde, considerando o status de autorização simulado. Medicamentos não autorizados (simulados) devem ser indicados como potenciais glosas ou excluídos do cálculo final (a ser definido).
(Opcional) Calcular o custo das visitas médicas, multiplicando o número de visitas pelo valor correspondente na Tabela Médica do IPASGO Saúde. A inclusão ou não deste item no cálculo padrão da conta hospitalar será um parâmetro a ser definido.
Apresentar o resultado da simulação:
Exibir um resumo da conta simulada, detalhando os custos por categoria: Diárias, Taxas Hospitalares, Procedimentos, Materiais, Medicamentos (e, opcionalmente, Visitas Médicas).
Listar os códigos e descrições dos itens faturados, bem como as quantidades e valores unitários e totais.
Mostrar o valor total final da conta simulada.
Indicar visualmente ou por meio de notas os itens que seriam potencialmente glosados na simulação devido à falta de autorização prévia simulada.
Informar a data de referência das tabelas do IPASGO Saúde utilizadas na simulação.
6. Requisitos Não Funcionais

Usabilidade:
A interface do usuário deve ser clara, intuitiva e fácil de usar, mesmo para usuários sem experiência prévia em faturamento hospitalar.
A navegação entre as seções de entrada de dados e a visualização dos resultados deve ser simples e eficiente.
Informações contextuais ou dicas podem ser fornecidas para auxiliar o usuário no preenchimento dos dados.
Performance:
O aplicativo deve ser rápido e responsivo, com tempos de carregamento mínimos para as páginas e cálculos.
Acessibilidade:
O aplicativo deve ser desenvolvido considerando as diretrizes de acessibilidade web (WCAG) para garantir que possa ser utilizado por pessoas com diferentes necessidades.
Manutenibilidade:
A arquitetura do aplicativo (Next.js) deve facilitar a manutenção e atualização do código.
Os dados das tabelas do IPASGO Saúde devem ser gerenciados de forma que atualizações futuras das tabelas possam ser implementadas de maneira eficiente.
Segurança:
Considerando que o aplicativo é de acesso público ("DeepSite") e o objetivo principal é a simulação educacional, a segurança focará em proteger a integridade do aplicativo e evitar vulnerabilidades comuns em aplicações web. Não haverá tratamento de dados pessoais sensíveis de pacientes.
Escalabilidade:
Embora o foco inicial seja em internações de curta duração, a arquitetura deve considerar a potencial expansão futura para incluir outros cenários de faturamento (ex: internações mais longas, atendimentos ambulatoriais).
Confiabilidade:
Os cálculos realizados pelo simulador devem ser precisos e consistentes, seguindo a lógica definida com base nas regras e tabelas do IPASGO Saúde.
Portabilidade:
Sendo um aplicativo web desenvolvido com Next.js, ele deverá ser acessível através de diferentes navegadores e dispositivos (desktops, tablets, smartphones).
7. Restrições

O desenvolvimento do simulador deve se basear nas informações contidas no documento "Simulação de Internação. D.1 (1).pdf" e nas tabelas e normativas do IPASGO Saúde referenciadas neste documento [1, 8, 9, 16, 17, 18, etc.].
Devido à ausência de regras explícitas publicamente disponíveis para o cálculo do número de diárias pelo IPASGO Saúde, o aplicativo deverá implementar uma regra configurável pelo usuário ou adotar uma premissa de mercado comum, com a devida informação ao usuário sobre a regra utilizada.
O simulador deverá focar em um subconjunto gerenciável de códigos TUSS/IPASGO representativos de internações de curta duração para evitar complexidade excessiva. A seleção deste subconjunto será definida em etapas posteriores do projeto.
O aplicativo não terá integração direta com os sistemas do IPASGO Saúde (Facplan, SAAT, etc.). Os dados utilizados serão baseados nas tabelas e informações publicadas.
O simulador não contemplará regras específicas de auditoria do IPASGO Saúde em detalhes, mas indicará potenciais glosas por falta de autorização simulada.
O aplicativo não incluirá funcionalidades de autenticação ou armazenamento de dados de simulação entre sessões de usuários, dada a sua natureza pública e educacional.
8. Critérios de Aceitação

O aplicativo será considerado aceito quando atender aos seguintes critérios:

Todas as funcionalidades descritas nos Requisitos Funcionais estiverem implementadas e funcionando corretamente.
Os cálculos realizados pelo simulador estiverem de acordo com a lógica definida e utilizando os dados das tabelas do IPASGO Saúde (nas versões de referência utilizadas).
A interface do usuário for considerada intuitiva e de fácil utilização pelo público-alvo (a ser validado por testes de usabilidade).
O aplicativo atender aos requisitos não funcionais de performance e acessibilidade definidos.
O código do aplicativo estiver bem estruturado e documentado, facilitando a manutenção futura.
A regra de cálculo de diárias estiver claramente definida e, se configurável, funcionando conforme o esperado.
As informações sobre as tabelas do IPASGO Saúde utilizadas (data de referência) e a distinção entre conta hospitalar e honorários médicos estiverem claramente apresentadas ao usuário.
9. Referências

Este documento de especificação foi elaborado com base nas informações contidas nos seguintes documentos:

Excertos de "Simulação de Internação. D.1 (1).pdf" (análise detalhada do processo de faturamento).
www.ipasgo.go.gov.br, acessado em abril 18, 2025, https://www.ipasgo.go.gov.br/files/Tabela-de-Servicos-Hospitalares/TabelaServicosHospitalares042025.pdf (Exemplo de Tabela de Serviços Hospitalares).
www.ipasgo.go.gov.br, acessado em abril 18, 2025, https://www.ipasgo.go.gov.br/files/Tabela-de-Materiais-Medicamentos/MateriaisMedicamentos022023.pdf (Exemplo de Tabela de Materiais e Medicamentos).
Tabela de Procedimentos Médicos IPASGO SAÚDE 08/2024, acessado em abril 18, 2025, https://www.ipasgo.go.gov.br/files/Tabela-Medica-Ipasgo/TabelaMedicaIpasgo082024.pdf (Exemplo de Tabela Médica).
www.ipasgo.go.gov.br, acessado em abril 18, 2025, https://www.ipasgo.go.gov.br/files/Tabela-Medica-Ipasgo/TabelaMedicaIpasgo022025.pdf (Exemplo de Tabela Médica com códigos de visitas).
LISTAGEM DE MATERIAIS E MEDICAMENTOS REFERÊNCIA 04/2025, acessado em abril 18, 2025, https://www.ipasgo.go.gov.br/files/Tabela-de-Materiais-Medicamentos/MateriaisMedicamentos042025.pdf (Exemplo de Tabela de Materiais e Medicamentos).
www.ipasgo.go.gov.br, acessado em abril 18, 2025, https://www.ipasgo.go.gov.br/files/Arquivos/Conta_Nosocomial.pdf (Referência à Conta Nosocomial).
Seção VI do documento base ("Lógica do Motor de Cálculo").
Seção VII do documento base ("Recomendações para o Aplicativo" - subconjunto de códigos e regra de cálculo de diárias).
Seção VII do documento base ("Recomendações para o Aplicativo" - clarificação do escopo).
