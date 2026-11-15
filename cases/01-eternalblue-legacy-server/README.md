# Estudo de Caso 01 — Gestão de risco em servidor legado vulnerável ao EternalBlue

**Tema:** CVE-2017-0144 / Microsoft SMBv1  
**Categoria:** Gestão de vulnerabilidades e risco  
**Classificação utilizada no caso original:** Alta  
**Natureza:** Estudo de caso profissional anonimizado e adaptado

## 1. Contexto

Durante atividades de monitoramento e gestão de vulnerabilidades, foi identificada exposição associada à CVE-2017-0144 em um servidor legado utilizado por serviços de produção.

A CVE-2017-0144 está relacionada a uma vulnerabilidade de execução remota de código no servidor SMBv1 do Microsoft Windows. A Microsoft publicou a atualização de segurança MS17-010 para corrigir vulnerabilidades dessa família. O EternalBlue ficou amplamente associado à exploração de falhas SMBv1, inclusive em campanhas como WannaCry.

A versão exata do sistema operacional e os identificadores do ativo foram omitidos. Em uma validação técnica, a confirmação da exposição deve estar apoiada em inventário, versão/build do sistema, estado do SMBv1, histórico de atualizações e evidências do mecanismo de detecção utilizado.

## 2. Objetivo da análise

- Delimitar a exposição do ativo legado.
- Avaliar o risco para um servidor que sustentava serviços produtivos.
- Identificar medidas compensatórias aplicáveis sem interromper imediatamente o serviço.
- Recomendar um caminho de correção definitiva.

## 3. Condições observadas

- Sistema operacional legado, fora do ciclo regular de suporte.
- Ausência de solução EDR ou de proteção avançada de endpoint identificada no cenário analisado.
- Exposição associada a vulnerabilidade conhecida de execução remota de código.
- Ativo utilizado em produção, com dependência operacional que limitava seu desligamento imediato.

A ausência de EDR não é a causa da vulnerabilidade, mas reduz a capacidade de prevenção, detecção e resposta no endpoint, aumentando a relevância dos controles compensatórios.

## 4. Avaliação de risco

O risco foi considerado elevado pela combinação entre exposição técnica, relevância operacional do servidor e limitações de suporte e proteção do endpoint.

A classificação **Alta** representa a avaliação registrada para o cenário descrito; não deve ser interpretada como uma pontuação CVSS calculada para o ativo. A severidade de uma CVE e o risco efetivo de um ativo dependem também de exposição, contexto, criticidade, controles existentes e possibilidade de exploração.

Não há, no material disponibilizado para este portfólio, evidência de exploração bem-sucedida ou de comprometimento do servidor. O foco deste caso é a gestão da exposição e do risco.

## 5. Medidas de contenção registradas

- Restrição do acesso direto à Internet para o ativo.
- Reforço do monitoramento de segurança.
- Criação de regras específicas para identificar atividades suspeitas relacionadas ao cenário.
- Acompanhamento contínuo do comportamento do servidor.

Essas medidas reduziram a exposição enquanto a correção estrutural era planejada. Elas não substituem a aplicação de correções, a atualização do sistema ou a desativação de componentes vulneráveis.

## 6. Recomendações técnicas

1. Planejar a substituição do servidor por uma plataforma suportada.
2. Aplicar as atualizações de segurança pertinentes e validar a correção da CVE.
3. Avaliar a desativação do SMBv1 quando não houver dependência operacional legítima.
4. Implementar EDR e controles de hardening compatíveis com a plataforma.
5. Restringir o acesso SMB por segmentação e regras de firewall, permitindo somente origens necessárias.
6. Documentar dependências, responsáveis, prazo de migração e critérios de encerramento do risco.

## 7. Gestão do risco residual

Como o ativo possuía relevância operacional, foi adotado um aceite temporário de risco, condicionado à manutenção dos controles compensatórios e à existência de um plano de substituição.

O aceite temporário deve ser formalizado pelo responsável competente, ter prazo e responsável definidos, critérios de revisão e condições claras para encerramento. O material de origem informa a existência do aceite e do plano, mas não confirma a conclusão da migração; por isso, este portfólio não declara que a substituição foi concluída.

## 8. Conclusão

O caso demonstra que a gestão de uma vulnerabilidade crítica em um ativo legado não se limita à identificação da CVE. A decisão exige avaliar a criticidade do serviço, as dependências operacionais, os controles compensatórios e a viabilidade de uma remediação definitiva.

A abordagem registrada combinou redução imediata da exposição, monitoramento reforçado, aceite temporário do risco e planejamento de substituição do ativo.

## 9. Competências demonstradas

- Gestão de vulnerabilidades e avaliação de risco.
- Conhecimento de SMBv1 e CVE-2017-0144.
- Definição de controles compensatórios.
- Comunicação de risco e alinhamento operacional.
- Planejamento de remediação e tratamento de risco residual.

## 10. Referências

- [NIST National Vulnerability Database — CVE-2017-0144](https://nvd.nist.gov/vuln/detail/CVE-2017-0144)
- [Microsoft Security Bulletin MS17-010](https://learn.microsoft.com/pt-br/security-updates/securitybulletins/2017/ms17-010)

## Limitações

Este estudo não publica versão do sistema, evidências de scanner, regras de firewall, logs, endereços de rede ou identificadores do ativo. A confirmação técnica e o encerramento da vulnerabilidade devem ser demonstrados por evidências próprias do ambiente, que não fazem parte deste portfólio.
