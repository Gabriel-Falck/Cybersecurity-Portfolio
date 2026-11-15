# Estudo de Caso 04 — Uncommon Process Anomaly em ambiente Linux

**Tema:** Análise comportamental de processos em Linux  
**Categoria:** Threat Detection, Threat Hunting e validação de alertas  
**Resultado registrado:** Falso positivo contextualizado no escopo investigado  
**Natureza:** Estudo de caso profissional anonimizado e adaptado

## 1. Contexto

Durante operações de monitoramento de segurança em servidores Linux, foram identificados múltiplos alertas classificados como `Uncommon Process Anomaly`. Esse tipo de alerta indica execução de processos fora do padrão histórico observado para determinado ativo ou contexto.

A ocorrência de um processo incomum não significa necessariamente atividade maliciosa. O alerta demanda validação de contexto, principalmente em servidores que executam agentes de gerenciamento, monitoramento e automação.

## 2. Objetivo da análise

- Entender por que os processos foram sinalizados como incomuns.
- Avaliar recorrência, contexto operacional e relação com contas de serviço.
- Identificar sinais que justificassem escalonamento ou resposta a incidente.
- Evitar contenção desnecessária de atividades legítimas.

## 3. Análise realizada

A investigação considerou os seguintes aspectos descritos no material de origem:

- Distribuição temporal dos eventos e recorrência em janelas específicas.
- Concentração dos alertas em servidores associados a funções de infraestrutura e gerenciamento.
- Execução vinculada a contas de serviço.
- Relação entre os comandos observados e rotinas conhecidas de agentes legítimos de gerenciamento.
- Compatibilidade do comportamento observado com atividades operacionais previamente documentadas.

A repetição em horários semelhantes pode indicar automação, mas não é evidência suficiente de legitimidade. A conclusão depende da correlação com a função do ativo, o processo responsável e a rotina esperada.

## 4. Resultado da validação

Após a contextualização dos eventos e a correlação com as rotinas operacionais conhecidas, as execuções foram associadas a agentes legítimos de gerenciamento e monitoramento.

Os alertas foram classificados como **False Positive (falso positivo) no escopo analisado**. No conjunto de evidências descrito, não foram identificados indícios de execução de malware, escalada de privilégios, persistência maliciosa ou comunicação externa suspeita relacionados aos eventos investigados.

Essa classificação não significa que todos os processos do servidor ou todo o ambiente tenham sido auditados. Ela se limita aos eventos e dados considerados na investigação.

## 5. Boas práticas para casos semelhantes

- Verificar processo pai/filho, linha de comando, usuário e contexto de execução.
- Comparar a atividade com inventário de software e documentação operacional.
- Validar proprietário, função e frequência esperada do agente.
- Correlacionar a execução com alterações de arquivos, conexões de rede e eventos de autenticação.
- Registrar a justificativa da classificação para permitir revisão futura.
- Ajustar regras ou exceções de detecção somente com escopo restrito, justificativa e acompanhamento.

## 6. Conclusão

O estudo demonstra que alertas comportamentais precisam ser investigados à luz do contexto operacional. A validação de processos legítimos reduz falsos positivos e evita ações disruptivas, sem dispensar a preservação de evidências e o monitoramento contínuo.

## 7. Competências demonstradas

- Análise comportamental de processos Linux.
- Threat Hunting orientado a contexto.
- Correlação temporal de eventos.
- Validação de contas de serviço e rotinas operacionais.
- Classificação fundamentada de falsos positivos.

## 8. Tecnologias e conceitos

- Plataforma XDR (categoria tecnológica; fabricante não divulgado).
- Monitoramento de endpoints Linux.
- Detecção comportamental de processos.
- Threat Hunting e triagem de alertas.

## Limitações

Nomes de servidores, usuários, processos específicos, comandos completos, horários e detalhes dos agentes foram omitidos. A classificação de falso positivo se restringe ao conjunto de eventos descrito e não constitui garantia geral de integridade do host.
