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
