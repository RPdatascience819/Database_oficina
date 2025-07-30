# Database_oficina
Suzano - Análise de Dados com Power BI - Database conceitual

# Contexto do Projeto
O objetivo é criar um sistema para controlar o fluxo de trabalho de uma oficina, desde a chegada do veículo do cliente até a conclusão do serviço. O sistema deve gerenciar clientes, seus veículos, as equipes de mecânicos responsáveis, e as ordens de serviço (OS) que detalham os serviços a serem executados e as peças a serem utilizadas.

# A narrativa base para a modelagem foi:

Clientes levam veículos à oficina mecânica para serem consertados ou para passarem por revisões periódicas. Cada veículo é designado a uma equipe de mecânicos que identifica os serviços a serem executados e preenche uma OS com data de entrega. A partir da OS, calcula-se o valor de cada serviço, consultando-se uma tabela de referência de mão-de-obra. O valor de cada peça também irá compor a OS. O cliente autoriza a execução dos serviços. A mesma equipe avalia e executa os serviços. Os mecânicos possuem código, nome, endereço e especialidade. Cada OS possui: n°, data de emissão, um valor, status e uma data para conclusão dos trabalhos.

# Descrição do Esquema Conceitual
O esquema foi projetado para ser normalizado e relacional, garantindo a integridade e a consistência dos dados. As principais entidades são:

* Cliente: Armazena as informações dos proprietários dos veículos.

* Veiculo: Contém os detalhes de cada veículo, com uma referência direta ao seu proprietário (Cliente).

* Equipe: Define as equipes de trabalho. Foi criada como uma entidade separada para permitir que uma equipe seja composta por vários mecânicos.

* Mecanico: Cadastro individual de cada mecânico com seus dados e especialidade.

* OrdemServico: A tabela central que conecta Veiculo, Equipe e os detalhes do serviço. Controla o status, datas e valores.

* Servico e Peca: Tabelas de referência (lookup tables) que funcionam como um catálogo de serviços e peças com seus respectivos valores.

# Tabelas Associativas:

Mecanico_Equipe: Permite um relacionamento N:M entre mecânicos e equipes.

OS_Servicos: Liga uma Ordem de Serviço aos vários serviços que ela pode conter.

OS_Pecas: Liga uma Ordem de Serviço às várias peças utilizadas, incluindo a quantidade.

# Suposições e Decisões de Projeto
Durante a modelagem, algumas decisões foram tomadas para complementar a narrativa:

Identificadores Únicos: Foram adicionados campos de identificação única como CPF para Cliente, Placa para Veiculo e CodigoMecanico para Mecanico, para evitar duplicidade de registros.

Status da OS: Foi utilizado um tipo ENUM para o campo StatusOS na tabela OrdemServico. Isso restringe os valores possíveis a um conjunto pré-definido ('Aguardando Aprovação', 'Aprovada', 'Em Execução', 'Concluída', 'Cancelada'), garantindo consistência.

Autorização do Cliente: Foi incluído um campo booleano AutorizacaoCliente na OrdemServico para registrar explicitamente a aprovação do cliente, um passo crucial mencionado na narrativa.

Relacionamento Mecânico-Equipe: Optei por uma relação N:M para oferecer mais flexibilidade ao sistema, permitindo que um mecânico possa ser associado a múltiplas equipes no futuro.
