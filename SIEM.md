## SIEM - Security Information and Event Management    


Uma solução de segurança cibernética que coleta, analisa e correlaciona logs e eventos de diferentes sistemas de TI em tempo real, com o objetivo de detectar, responder e reportar atividades suspeitas ou maliciosas.  

Em detalhes:  
SI → Security Information: refere-se à coleta e centralização de dados de segurança, como logs de firewall, servidores, endpoints, antivírus, etc.  

EM → Event Management: trata da análise dos eventos em tempo real, identificando comportamentos anômalos, falhas ou possíveis ataques.  

Funcionalidades principais:  
Coleta de logs: Recebe dados de várias fontes (firewalls, sistemas operacionais, IDS/IPS, aplicações).  
  
Correlação de eventos: Analisa padrões para detectar possíveis ameaças.  
  
Alertas em tempo real: Gera notificações quando algo suspeito acontece.  
  
Dashboards e relatórios: Facilita a visualização e auditoria dos dados.  
  
Resposta a incidentes: Pode integrar com outras ferramentas para automatizar respostas (como isolar um host infectado).  
  
Lista de SIEM á se testar:  
Splunk  
IBM QRadar  
  
ArcSight (Micro Focus)  
  
LogRhythm  
  
Elastic Security (ELK Stack com SIEM)  
  
Pra que serve?
Detectar ataques cibernéticos (ex: brute force, movimentações laterais).  
  
Ajudar no atendimento à conformidade, como ISO 27001, LGPD, PCI-DSS.  
  
Investigar incidentes após o ocorrido (forense).  
  
Monitorar o ambiente de forma centralizada.  
 

# Aplicação: 
Tentativa de ataque por força bruta em um servidor  
   
Ambiente:  
  
Empresa com 200 funcionários.  
Tem um servidor web (Linux) acessado remotamente por SSH.  
Utiliza o SIEM Splunk para monitoramento centralizado.   
Todos os dispositivos (firewall, servidor, endpoint, antivírus) enviam logs para o SIEM.  
  
Etapas do funcionamento do SIEM nesse cenário:  
  
1. Coleta de dados  
O SIEM está coletando logs de:  
-Servidor SSH (/var/log/auth.log)  
-Firewall (registros de tentativas de conexão)  
-Antivírus e EDR dos computadores da equipe  
  
2. Correlações e regras ativas  
Foi configurada a seguinte regra no SIEM:  
“Se houver mais de 10 tentativas de login SSH com falha em 1 minuto a partir do mesmo IP → gerar alerta de ataque por força bruta.”  
  
3. Evento ocorre
Um atacante tenta invadir o servidor via SSH, usando nomes e senhas comuns (admin, root, etc.). Ele tenta 50 vezes em 30 segundos.  
  
4. O SIEM detecta e alerta  
O Splunk recebe os logs do servidor e identifica:  
50 falhas de login em menos de 1 minuto  
Todas vindas do mesmo IP  
O IP não é conhecido ou confiável  
Resultado: Um alerta é gerado automaticamente no painel do analista de segurança.  
  
5. Ação de resposta  
O analista recebe o alerta e investiga.  
Vê que o IP é da Rússia e decide bloquear o IP no firewall manualmente (ou o SIEM já poderia ter feito isso via playbook automatizado com SOAR).  
Também configura para banir IPs automaticamente com esse comportamento no futuro.  
  
6. Registro e relatório
O incidente é documentado no sistema.  
Um **relatório** é gerado com detalhes do ataque e da resposta.  
Esse relatório ajuda em futuras auditorias e conformidade com normas como a ISO 27001.  


