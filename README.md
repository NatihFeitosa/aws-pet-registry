# Projeto de Arquitetura AWS: Clínica Veterinária

### Descrição do Projeto

Este projeto demonstra uma arquitetura básica na AWS para um sistema de cadastro de animais em uma clínica veterinária. A solução utiliza quatro serviços-chave da AWS para gerenciar e processar o upload de fotos de animais de forma automática e eficiente.

### Componentes da Arquitetura

O diagrama de arquitetura, localizado na pasta `/images` deste repositório, ilustra o fluxo de dados e a interação entre os seguintes serviços da AWS:

* **Amazon S3 (Simple Storage Service):** Utilizado para armazenar as fotos dos animais. Ele também atua como um ponto de entrada para o processamento, disparando um evento quando uma nova foto é carregada.
* **AWS Lambda:** Uma função serverless acionada pelo evento de upload de foto no S3. O Lambda é responsável por processar a foto automaticamente, realizando tarefas como redimensionamento, aplicação de filtros ou qualquer outra manipulação necessária.
* **Amazon EC2 (Elastic Compute Cloud):** Uma instância de máquina virtual que hospeda a aplicação principal do sistema de cadastro da clínica. É o servidor onde o software da clínica está instalado e em execução.
* **Amazon EBS (Elastic Block Store):** Um volume de armazenamento persistente que é anexado à instância EC2. Ele é usado como o disco interno para guardar o banco de dados da aplicação e os logs de execução.

### Fluxo de Dados

1.  Um **Usuário** acessa o **Sistema da Clínica** (hospedado no EC2) para cadastrar um novo animal.
2.  A aplicação no **EC2** solicita ao usuário o **upload de fotos**.
3.  A foto é enviada diretamente para um bucket no **Amazon S3**.
4.  O evento de "nova foto criada" no S3 dispara a execução de uma função no **AWS Lambda**.
5.  A função **Lambda** processa a foto e salva a versão processada de volta no **S3**.
6.  A aplicação no **EC2** salva os dados do animal e os metadados das fotos no banco de dados, que está no volume **EBS** conectado à instância.

### Documentação Adicional

* **Diagrama de Arquitetura:** Você pode encontrar o diagrama de arquitetura na pasta `images/` deste repositório.
* **Decisões de Design:** Embora a arquitetura utilize componentes específicos para o desafio, ela ilustra um fluxo de trabalho comum para o processamento assíncrono de arquivos na AWS.
