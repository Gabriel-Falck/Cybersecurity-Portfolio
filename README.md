# Portfólio Técnico | Segurança da Informação

Estudos de caso sobre operações de segurança, investigação de alertas, Threat Hunting, análise de tráfego, inteligência de ameaças e gestão de vulnerabilidades.

> **Sobre este material:** os estudos foram elaborados a partir de experiências profissionais e adaptados para apresentação pública e aprendizado. Informações de clientes, ambientes, ativos, endereços internos, identificadores e detalhes operacionais foram removidos ou generalizados. Os exemplos não representam um cliente ou uma infraestrutura específica.

## Perfil técnico

Atuação em operações de segurança da informação, com foco em análise e triagem de eventos, investigação de comportamentos suspeitos, correlação de evidências, avaliação de risco e elaboração de recomendações técnicas.

## Estudos de caso

| # | Estudo | Principais competências demonstradas |
|---|---|---|
| 01 | [Gestão de risco em servidor legado — CVE-2017-0144 / EternalBlue](cases/01-eternalblue-legacy-server/) | Gestão de vulnerabilidades, risco residual, controles compensatórios e planejamento de remediação |
| 02 | [Tentativa de exploração JNDI — contexto Log4Shell](cases/02-jndi-log4shell/) | Análise de requisições HTTP, investigação de indicadores, validação de evidências e resposta a incidentes |
| 03 | [Tráfego SSH para destinos com reputação suspeita](cases/03-ssh-malicious-destinations/) | Threat Hunting, análise de tráfego, OSINT e controle de tráfego de saída |
| 04 | [Uncommon Process Anomaly em Linux](cases/04-uncommon-process-anomaly/) | Análise comportamental, contextualização de alertas e redução de falsos positivos |
| 05 | [Aumento de eventos associados à infraestrutura DigitalOcean](cases/05-digitalocean-threat-activity/) | Threat Intelligence, OSINT, correlação de indicadores e bloqueio seletivo |
| 06 | [Comunicação suspeita e tráfego relacionado ao Memcached](cases/06-memcached-suspicious-traffic/) | Análise de tráfego interno e externo, validação de serviços e mitigação de exposição |

## Competências abordadas

- Security Operations (SecOps) e análise de eventos de segurança
- Threat Detection, Threat Hunting e triagem de alertas
- Análise de tráfego de rede e protocolos
- Inteligência de ameaças (Threat Intelligence) e OSINT
- Indicadores de comprometimento (IOCs) e análise de reputação
- Gestão de vulnerabilidades e avaliação de risco
- Resposta a incidentes, contenção e recomendações de mitigação
- Análise comportamental de processos em Linux
- Documentação técnica e comunicação de risco

## Como os estudos estão organizados

Cada estudo apresenta contexto, objetivo, sinais observados, análise técnica, avaliação, ações/recomendações, conclusão e limitações. Quando uma medida foi apenas recomendada, isso é indicado expressamente; não se deve interpretar uma recomendação como confirmação de implementação.

## Limitações e responsabilidade

- Os textos são versões educacionais e resumidas de análises anonimizadas.
- Dados brutos, logs completos, nomes de clientes, IPs internos, hostnames, domínios privados, topologias, credenciais e evidências identificáveis não são publicados.
- Indicadores públicos podem mudar de reputação ou deixar de ser relevantes. Por isso, listas históricas de IPs foram omitidas.
- A presença de um alerta, payload ou indicador isolado não comprova comprometimento. As conclusões são limitadas às evidências descritas em cada estudo.
- Este repositório não substitui uma investigação forense, uma avaliação independente ou a documentação operacional do ambiente analisado.

## Idioma

O conteúdo principal está em português, mantendo termos técnicos amplamente utilizados em inglês. Uma versão em inglês poderá ser adicionada posteriormente.
