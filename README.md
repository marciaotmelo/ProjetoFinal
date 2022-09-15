# ProjetoFinal
 ProjetoFinalDio_Oficina


Neste desafio, você irá utilizar seu esquema conceitual, criado no desafio do módulo de modelagem de BD com modelo ER, para criar o esquema lógico para o contexto de uma oficina. Você definirá todas as etapas. Desde o esquema até a implementação do banco de dados.

![Oficina_Mecânica](https://user-images.githubusercontent.com/108886670/190289776-2123fcc0-0d96-482e-a96f-f36de85add2e.png)

__Implementação do banco de dados__

CREATE DATABASE oficina;
USE oficina;
-- Criar a tabela cliente

CREATE TABLE cliente (
  idCliente INT primary key,
  Nome VARCHAR(45) NOT NULL,
  CPF VARCHAR(11) NOT NULL,
  Contato VARCHAR(15) NULL,
  Endereco VARCHAR(45));
  
 drop table pecas;
  
  -- Criar a tabela mecanico
  CREATE TABLE mecanico (
  idMecanico INT primary key,
  Nome VARCHAR(45) NOT NULL,
  Contato VARCHAR(11)  NULL,
  Especialidade VARCHAR(15) NULL,
  Endereco VARCHAR(45));
  
  -- Criar a tabela pecas
  CREATE TABLE pecas (
  idPecas INT primary key,
  Tipo VARCHAR(45) NOT NULL,
  Valor FLOAT NOT NULL,
  Quantidade INT);
  
  -- Criar a tabela especialidade
  CREATE TABLE especialidade (
  idEspecialidade INT primary key,
  Descricao VARCHAR(100) NULL,
  ValorMaodeObra FLOAT NOT NULL,
  CONSTRAINT fk_idMecanico_mecanico
  FOREIGN KEY (idEspecialidade)
  REFERENCES oficina.Mecanico(idMecanico));
  
     
  -- Criar a tabela serviço
  CREATE TABLE servico (
  idServico INT primary key,
  Categoria VARCHAR(45) NULL,
  Descricao VARCHAR(100) NULL,
  DataEmissao DATE,
  DataConclusao DATE,
  CONSTRAINT fk_servico_especialidade
  FOREIGN KEY (idServico)
  REFERENCES oficina.especialidade(idEspecialidade));
  
   -- Criar a tabela Ordem de Serviço
  CREATE TABLE OrdemServico (
  idOrdemServico INT primary key,
  DataEmissao DATE,
  Diagnostico VARCHAR(200) NOT NULL,
  SolucaoAplicada VARCHAR(150) NOT NULL,
  ValorTotal FLOAT,
  PecasTrocadas VARCHAR(80) NULL,
  DataConclusao DATE,
  Statuss VARCHAR(80),
  CONSTRAINT fk_Ordemservico_especialidade
  FOREIGN KEY (idOrdemServico)
  REFERENCES oficina.especialidade(idEspecialidade));
  
   -- Criar a tabela Autorização
  CREATE TABLE Autoriza (
  idAutoriza INT primary key,
  Pagamento VARCHAR(45),
  CONSTRAINT fk_Autoriza_cliente FOREIGN KEY (idAutoriza) REFERENCES oficina.cliente(idCliente),
  CONSTRAINT fk_Autoriza_servico FOREIGN KEY (idAutoriza) REFERENCES oficina.servico(idServico));
  
  -- Criar a tabela Equipe Responsável
  CREATE TABLE EquipeResponsavel (
  idEquipeResponsavel INT primary key,
  Dataservico DATE,
  Observacao VARCHAR(150),
  CONSTRAINT fk_EquipeResponsavel_OrdemServico FOREIGN KEY (idEquipeResponsavel) REFERENCES oficina.OrdemServico(idOrdemServico),
  CONSTRAINT fk_EquipeResponsavel_Servico FOREIGN KEY (idEquipeResponsavel) REFERENCES oficina.servico(idServico));
  
  
  -- Criar a tabela Veículos
  CREATE TABLE Veiculo (
  idVeiculo INT primary key,
  Ano INT,
  Modelo VARCHAR(45),
  Categoria VARCHAR(45),
  Cor VARCHAR(20),
  CONSTRAINT fk_Veiculo_Cliente FOREIGN KEY (idVeiculo) REFERENCES oficina.Cliente(idCliente),
  CONSTRAINT fk_Veiculo_EquipeResponsavel FOREIGN KEY (idVeiculo) REFERENCES oficina.EquipeResponsavel(idEquipeResponsavel));
