# Estudo de Caso 03 — Tráfego SSH de origem interna para destinos com reputação suspeita

**Tema:** SSH / TCP 22 / análise de reputação e tráfego de saída  
**Categoria:** Threat Hunting e análise de tráfego de rede  
**Natureza:** Estudo de caso profissional anonimizado e adaptado

## 1. Contexto

Durante atividades de Threat Hunting, foram identificadas tentativas de comunicação SSH originadas de ativos internos com destino a endereços IP externos que apresentavam reputação suspeita em fontes públicas de inteligência, incluindo VirusTotal e AbuseIPDB.

Os endereços, provedores, ASN e demais identificadores externos foram omitidos desta versão. Reputações de IP são dinâmicas e precisam ser consultadas novamente no momento de uma investigação; a classificação registrada em uma data não deve ser tratada como permanente.

## 2. Objetivo da análise

- Avaliar se o tráfego SSH de saída era esperado e autorizado.
- Correlacionar os destinos com fontes públicas de reputação.
- Interpretar os estados das conexões observados na telemetria.
- Recomendar ações proporcionais às evidências disponíveis.

## 3. Padrões observados

O material analisado descreveu conexões classificadas pela plataforma de monitoramento como:

- **Abortadas:** tentativas encerradas antes da conclusão da comunicação.
- **Expiradas:** tentativas sem resposta dentro do período esperado.
- **Half-opened:** conexões iniciadas, mas sem conclusão do estabelecimento TCP.
- **NoSYN:** ausência de pacote SYN observado na telemetria coletada.

A semântica exata desses estados pode variar conforme a ferramenta e a forma de coleta. Em particular, a ausência de SYN no conjunto de dados não prova que nenhum SYN existiu na rede: assimetria de roteamento, perda de pacotes, amostragem ou limitações de visibilidade podem influenciar a captura.

### Consulta a fontes de inteligência (OSINT)

Durante a investigação, foram consultados indicadores de endereços IP em fontes públicas de inteligência, incluindo VirusTotal e AbuseIPDB.

Os resultados apresentaram divergências entre as plataformas: alguns indicadores não possuíam detecções relevantes no VirusTotal, mas apresentavam registros ou denúncias no AbuseIPDB. Essas diferenças reforçam que as fontes devem ser interpretadas de forma complementar, considerando seus critérios e limitações.

A ausência de detecções em uma plataforma não comprova reputação confiável, assim como registros de denúncias em outra não comprovam, isoladamente, atividade maliciosa.

## 4. Análise técnica

A correlação entre tráfego SSH de saída e indicadores com reputação negativa justifica investigação, mas não comprova, por si só, comprometimento do host interno.

É necessário verificar:

- Qual ativo, usuário, processo ou serviço iniciou a comunicação.
- Se o uso de SSH externo é legítimo para a função do ativo.
- Se houve resolução DNS, tentativa TCP, autenticação ou sessão SSH efetivamente estabelecida.
- Se existem eventos correlacionados em EDR, firewall, proxy, autenticação e logs do sistema.
- Se a reputação do destino é sustentada por múltiplas fontes e se o indicador ainda é relevante.

## 5. Avaliação do resultado

Na telemetria descrita no material de origem, não foi identificada conclusão bem-sucedida das conexões SSH analisadas. Isso reduz a evidência de uma sessão SSH estabelecida, mas não é suficiente para declarar o ativo de origem livre de comprometimento.

A hipótese de atividade automatizada, reconhecimento ou conexão residual deve permanecer como hipótese até ser corroborada por dados do ativo e da rede.

## 6. Ações recomendadas

1. Identificar os ativos internos de origem e os responsáveis por eles.
2. Correlacionar processo, usuário, comando, DNS, firewall e eventos de endpoint.
3. Confirmar se conexões SSH externas são necessárias para a operação.
4. Aplicar bloqueio seletivo aos indicadores confirmados como maliciosos, seguindo o processo de mudança e prevendo revisão/expiração da regra.
5. Restringir SSH de saída por política, permitindo somente origens e destinos autorizados.
6. Executar investigação ou varredura nos ativos quando houver sinais adicionais que justifiquem essa ação.
7. Criar alertas para recorrência, volume anômalo e destinos recém-identificados.

Bloqueios amplos por ASN, país ou provedor não devem ser recomendados somente com base em reputação de alguns endereços.

## 7. Conclusão

O caso demonstra a importância de monitorar tráfego de saída e correlacionar telemetria de rede com inteligência de ameaças. A reputação do destino funciona como contexto de investigação; o vínculo com um processo, usuário e ativo de origem é necessário para avaliar o risco e decidir a resposta.

## 8. Competências demonstradas

- Threat Hunting e análise de tráfego SSH.
- Interpretação de estados de conexão TCP.
- Consulta e correlação de fontes OSINT.
- Avaliação de risco baseada em evidências.
- Recomendações de controle de egress traffic.

## 9. Referências

- [RFC 9293 — Transmission Control Protocol (TCP)](https://www.rfc-editor.org/rfc/rfc9293)

## Limitações

A lista de IPs, ASN, provedores, horários, hosts e logs foi removida. As classificações de reputação são históricas e não foram reapresentadas como indicadores atuais. A interpretação dos estados deve ser conferida na documentação da plataforma de telemetria utilizada.
