
🚀 AWS Auto Scaling Lab (EC2 + ALB + AMI)

<img width="86" height="20" alt="image" src="https://github.com/user-attachments/assets/7c3cccbd-cc48-4ebd-a37c-ed5bd1ea6610" />
<img width="146" height="20" alt="image" src="https://github.com/user-attachments/assets/09a19e66-16ba-4066-a7a3-59286767e9a1" />

 AWS Auto Scaling Lab – EC2, Launch Template, Application Load Balancer & Auto Scaling Group





📖 Visão Geral do Projeto
Este projeto demonstra como implementar uma arquitetura altamente disponível e escalável utilizando Amazon EC2, Application Load Balancer (ALB) e Auto Scaling Group.

A solução distribui automaticamente o tráfego entre múltiplas instâncias EC2 e aumenta ou reduz a quantidade de servidores conforme a demanda, garantindo alta disponibilidade, escalabilidade e tolerância a falhas.

Essa arquitetura representa um dos modelos mais utilizados em ambientes de produção na AWS.

🎯 Objetivos
Criar uma AMI personalizada

Criar um Launch Template

Configurar um Auto Scaling Group

Configurar um Application Load Balancer

Criar Target Group

Distribuir requisições entre múltiplas instâncias

Configurar políticas automáticas de escala

Testar aumento e redução automática das instâncias

Garantir alta disponibilidade entre múltiplas zonas de disponibilidade



🏗 Arquitetura da Solução


                     Internet
                         │
                Application Load Balancer
                         │
          ┌──────────────┴──────────────┐
          │                             │
     EC2 Instance                  EC2 Instance
   (Availability Zone A)      (Availability Zone B)
          │                             │
          └──────────────┬──────────────┘
                         │
                 Auto Scaling Group
                         │
                 Launch Template
                         │
                    Amazon Machine Image





                     

⚙️ Serviços AWS Utilizados

| Serviço                    | Finalidade                         |
| -------------------------- | ---------------------------------- |
| Amazon EC2                 | Máquinas virtuais                  |
| Auto Scaling Group         | Escalabilidade automática          |
| Launch Template            | Modelo para criação das instâncias |
| Application Load Balancer  | Distribuição do tráfego            |
| Target Group               | Registro das instâncias            |
| Amazon Machine Image (AMI) | Imagem personalizada               |
| Security Groups            | Firewall                           |
| Amazon VPC                 | Rede Virtual                       |

🛠 Etapas de Implementação
Passo 1 – Criar uma Instância EC2
Foi criada uma instância EC2 utilizando Amazon Linux.

Configuração
| Parâmetro           | Valor        |
| ------------------- | ------------ |
| Sistema Operacional | Amazon Linux |
| Tipo                | t2.micro     |
| IP Público          | Ativado      |
| Security Group      | HTTP + SSH   |
Essa instância foi utilizada para instalar e configurar o servidor Web.

Passo 2 – Configurar o Servidor Web
Foi instalado o Apache.
sudo yum update -y
sudo yum install httpd -y
sudo systemctl enable httpd
sudo systemctl start httpd

Passo 3 – Criar uma AMI
Após configurar o servidor, foi criada uma Amazon Machine Image (AMI).

Objetivo:

reutilizar a configuração

automatizar novas instâncias

garantir padronização

Passo 4 – Criar um Launch Template
Foi criado um Launch Template utilizando a AMI personalizada.
| Parâmetro      | Valor         |
| -------------- | ------------- |
| AMI            | Personalizada |
| Tipo           | t2.micro      |
| Security Group | Web Server    |
| Key Pair       | Configurada   |

Passo 5 – Criar um Target Group
Foi criado um Target Group para registrar automaticamente as instâncias criadas pelo Auto Scaling Group.

Health Check:


/
Protocolo:


HTTP
Porta:


80
Passo 6 – Criar o Application Load Balancer
Foi criado um ALB público.

Configuração:

Internet Facing

HTTP

Porta 80

Target Group associado

Função:

Distribuir automaticamente as requisições entre todas as instâncias EC2.

Passo 7 – Criar o Auto Scaling Group
Foi criado um Auto Scaling Group utilizando o Launch Template.

Configuração
Configuração	Valor
Desired Capacity	2
Minimum	2
Maximum	4

Distribuição entre duas Availability Zones.

Passo 8 – Configurar Política de Escalabilidade
Foi criada uma política baseada na utilização da CPU.

Exemplo:

CPU > 70% → adiciona uma instância

CPU < 30% → remove uma instância

Passo 9 – Testar o Auto Scaling
Durante o laboratório foi realizado o teste de carga.

Resultado esperado:

novas instâncias criadas automaticamente

registradas automaticamente no Target Group

recebem tráfego do Load Balancer

Passo 10 – Teste de Alta Disponibilidade
Foi encerrada manualmente uma instância EC2.

Resultado:

o Auto Scaling detectou a falha

criou automaticamente outra instância

registrou no Load Balancer

restaurou a capacidade desejada

🔐 Benefícios da Arquitetura
Alta disponibilidade

Balanceamento automático de carga

Escalabilidade automática

Recuperação automática de falhas

Menor tempo de indisponibilidade

Melhor utilização dos recursos

Arquitetura preparada para produção

📚 Conceitos Demonstrados
| Conceito                  | Descrição                       |
| ------------------------- | ------------------------------- |
| Amazon EC2                | Máquinas Virtuais               |
| AMI                       | Imagem personalizada            |
| Launch Template           | Modelo de implantação           |
| Auto Scaling Group        | Escalabilidade automática       |
| Application Load Balancer | Balanceamento de carga          |
| Target Group              | Registro das instâncias         |
| Health Check              | Monitoramento das instâncias    |
| Alta Disponibilidade      | Continuidade do serviço         |
| Elasticidade              | Ajuste automático de capacidade |

🎓 Resultados de Aprendizagem
Este laboratório proporcionou experiência prática em:

Implementação de arquiteturas escaláveis na AWS

Criação de AMIs personalizadas

Configuração de Launch Templates

Uso do Application Load Balancer

Configuração de Auto Scaling Group

Políticas de escalabilidade automática

Balanceamento de carga

Alta disponibilidade

Arquiteturas semelhantes às utilizadas em ambientes de produção

📂 Estrutura do Repositório

aws-auto-scaling-lab
│
├── README.md
│
├── images
│   ├── architecture-diagram.png
│   ├── ec2-instance.png
│   ├── launch-template.png
│   ├── auto-scaling-group.png
│   ├── load-balancer.png
│   ├── target-group.png
│   ├── scaling-policy.png
│   └── cloudwatch-monitoring.png
│
├── scripts
│   ├── install-apache.sh
│   └── user-data.sh
│
└── docs
    └── lab-notes.md

📌 Autor
Paulo Henrique

AWS Cloud Practitioner | AWS Solutions Architect (em formação) | Entusiasta de Cloud Computing, Linux e Automação

⭐ Se este projeto foi útil para você, considere dar uma estrela no repositório!


