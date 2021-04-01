# fargate-ecs-estudo
Nosso projeto do Terraform é composto pela seguinte estrutura: Deploy de aplicações Docker na AWS usando ECS e Fargate

├── modules
│ └── code_pipeline
│ └── ecs
│ └── networking
│ └── rds
├── pipeline.tf
├── production.tf
├── production_key.pub
├── terraform.tfvars
└── variables.tf


1° cria a VPC, 4 subnets (2 públicas e 2 privadas) em cada Availability Zone. Também cria o NAT para permitir a subnet privada acessar a internet

2°Banco somente REDE privada

3°LoadBalace Ele será colocado na subnet pública e irá enviar as requests para o Service no ECS.

4°Fargate nos permite escalar nossa aplicação facilmente. Para isso, precisamos apenas criar as métricas no CloudWatch e ativar os gatilhos para escalar para cima e para baixo.

5°politicas de Auto Scaling. Uma para escalar para cima e outra para escalar para baixo a quantidade desejada de Tasks rodando no nosso Service Web do ECS.
Depois criamos uma métrica no CloudWatch baseada no uso de CPU. Se o uso de CPU está maior que 85% por 2 períodos, a trigger de alarm_actionexecuta a política de Scale Up. Se retornar para o estado Ok, irá executar a política de Scale Down.


