## Projeto final Campinho AWS re/Start 🚀

Esse projeto foi desenvolvido como **Trabalho de Conclusão de Curso (TCC)** do programa **AWS re/Start**, simulando um cenário real de implantação de uma aplicação web escalável, segura e altamente disponível utilizando os principais serviços da AWS.

### Infraestrutura Obrigatória:

- ✅ Criar a infraestrutura de rede (VPC, sub-redes, route tables, IGW, etc.)
- ✅ Criar e configurar uma instância EC2 com Flask conectada ao RDS
- ✅ Criar uma imagem AMI da instância para uso no Auto Scaling Group
- ✅ Configurar um Launch Template + Auto Scaling Group
- ✅ Criar um Load Balancer (ALB) escutando na porta 5000
- ✅ Implantar a aplicação e garantir acesso via ALB
- ✅ Fazer um teste completo de failover e recuperação automática da aplicação

---

## Criar a infraestrutura de rede 

## VPC, sub-redes, route tables, IGW  
<img width="1418" height="676" alt="image" src="https://github.com/user-attachments/assets/b3f35e70-de15-4487-b03a-7cde4a681a0e" />
<img width="490" height="298" alt="image" src="https://github.com/user-attachments/assets/f89f1044-a77c-467f-ac77-500a3783814f" />
<img width="488" height="528" alt="image" src="https://github.com/user-attachments/assets/418bc604-9ee3-4cb7-81d1-7163c6c6902f" />
<img width="485" height="417" alt="image" src="https://github.com/user-attachments/assets/b466edf6-d5b1-4d25-b74d-67163cc490b7" />
<img width="1425" height="621" alt="image" src="https://github.com/user-attachments/assets/d33a4a9c-0369-4566-bb85-ee16c996d4df" />

---

## Security Group para EC2 e RDS  
<img width="1401" height="624" alt="image" src="https://github.com/user-attachments/assets/3f3c4bcf-624e-4bf0-beb3-34989e393c02" />
<img width="1401" height="622" alt="image" src="https://github.com/user-attachments/assets/2c9d4200-9d46-46a1-99bb-9db0a0915bbc" />
<img width="1183" height="251" alt="image" src="https://github.com/user-attachments/assets/10988092-1bd1-418f-aec5-740418d415fe" />

---

## Bando de dados  
<img width="1401" height="473" alt="image" src="https://github.com/user-attachments/assets/6c13e2d2-60f4-48ca-9dab-57b0c479f915" />
<img width="1384" height="622" alt="image" src="https://github.com/user-attachments/assets/f05ab3fe-3fa6-4309-bf92-2a9b34dfbe86" />

nome do banco de dados: db-projeto-final  
master username: adm  
senha: projetofinal2025  

<img width="1384" height="621" alt="image" src="https://github.com/user-attachments/assets/759b0ff6-4297-4ca7-965a-f17c66bfc966" />
<img width="1385" height="390" alt="image" src="https://github.com/user-attachments/assets/87cf68ba-d17b-4b35-842f-dd5f75ff04dc" />
<img width="1383" height="248" alt="image" src="https://github.com/user-attachments/assets/3efe8b64-1da9-4495-b797-a198ed0f8bc3" />
<img width="1387" height="403" alt="image" src="https://github.com/user-attachments/assets/53591f6c-c413-4966-b5d1-7c10a433dfc5" />
<img width="1381" height="227" alt="image" src="https://github.com/user-attachments/assets/df410b53-7fef-4c9c-b634-3e69d50bf891" />
Enhanced Monitoring > Backup > Maintenance (opcional desabilitar)

Banco de dados criado  
<img width="1429" height="244" alt="image" src="https://github.com/user-attachments/assets/aaef2795-697e-4237-8f87-af34d30e06fe" />

---

## Criar EC2 na Subnet Pública  

Nome da instãncia: Projeto-final-AWS  
<img width="948" height="654" alt="image" src="https://github.com/user-attachments/assets/8e97e6be-835f-4f46-a231-c3779ee7ed3d" />
<img width="916" height="256" alt="image" src="https://github.com/user-attachments/assets/5b6f231c-def5-4bc0-bb0f-70d011031a6c" />

Criação de uma Key pair: KeyPair-Projeto-final  
<img width="606" height="581" alt="image" src="https://github.com/user-attachments/assets/5d59b7bb-f88d-420d-9c50-75cf8f853bce" />
<img width="915" height="334" alt="image" src="https://github.com/user-attachments/assets/07ee2eaa-03db-4983-8d83-f13f0e1b1f62" />

<img width="917" height="589" alt="image" src="https://github.com/user-attachments/assets/4bb143e9-96cb-4cfd-8422-4b20142c439a" />

User data  
```
#!/bin/bash

# Atualiza e instala dependências
yum update -y
yum install -y git python3 python3-pip
sudo dnf install mariadb105 -y

# Cria o diretório onde o repositório será clonado
mkdir -p /home/ec2-user/TechStore2
cd /home/ec2-user/TechStore2

# Clona o repositório do GitHub
git clone https://github.com/HebertonGeovane/TechStore2.git .

# Instala as dependências do Python
pip3 install -r requirements.txt
pip3 install flask_sqlalchemy pymysql

# Exporta a variável de ambiente com o endpoint do RDS
export DATABASE_URL="mysql+pymysql://adm:projetofinal2025@db-projeto-final.ca6mam9wtria.us-west-2.rds.amazonaws.com/db-projeto-final" # Aqui você deve substituir 'SuaSenha', 'SeuEndpointRDS' e 'SeuNomeBanco' com as informações corretas do seu banco de dados.

# Cria o arquivo de configuração do Systemd
echo "[Unit]
Description=Flask Application
After=network.target

[Service]
User=ec2-user
WorkingDirectory=/home/ec2-user/TechStore2
ExecStart=/usr/bin/python3 /home/ec2-user/TechStore2/app.py
Restart=always
Environment=\"DATABASE_URL=mysql+pymysql://adm:projetofinal2025@db-projeto-final.ca6mam9wtria.us-west-2.rds.amazonaws.com/db-projeto-final\" # Aqui você deve substituir 'SuaSenha', 'SeuEndpointRDS' e 'SeuNomeBanco' com as informações corretas do seu banco de dados.

[Install]
WantedBy=multi-user.target" | sudo tee /etc/systemd/system/flaskapp.service

# Habilita o serviço para iniciar automaticamente
sudo systemctl enable flaskapp

# Inicia o serviço
sudo systemctl start flaskapp 
```

Instância criada:  
<img width="1420" height="248" alt="image" src="https://github.com/user-attachments/assets/55d7004e-c613-4203-8beb-139571b5b08a" />

Conectar a instância via SSH:  
<img width="1434" height="537" alt="image" src="https://github.com/user-attachments/assets/d14839ee-e72d-4c4a-8eca-d0763f862ba5" />







