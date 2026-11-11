# Planejamento dos Testes E2E com IA Generativa

Este documento registra o processo de planejamento, geração e refinamento dos testes End-to-End (E2E) para o aplicativo **React Native Crypto Alert**, utilizando modelos de Inteligência Artificial generativa e o framework de automação **Maestro**, em conformidade com as diretrizes do trabalho acadêmico.

---

## 1. Prompt Utilizado

```text
Atue como um Engenheiro de QA e Especialista em Automação Mobile com Maestro.
Analise a estrutura do aplicativo React Native Crypto Alert (Expo SDK 55, Expo Router, TypeScript).
O aplicativo possui as seguintes telas e funcionalidades:
1. Listagem de criptomoedas com preços, variação em 24h e badge de alertas.
2. Tela de conversão de valores entre criptomoedas e moedas fiduciárias (USD, BRL, EUR, GBP).
3. Tela de listagem de alertas de preço cadastrados e tela de criação de novos alertas com campo de preço alvo e condição (acima/abaixo).
4. Navegação por abas inferiores (Tabs: List, Convert, Alerts).

Proponha:
- Uma suíte de cenários de teste E2E independentes.
- Os passos de ação e asserção esperados para cada fluxo.
- A sintaxe inicial em formato YAML para execução com o Maestro CLI no emulador Android (appId: host.exp.exponent).
```

---

## 2. Resposta Original da IA

Abaixo está transcrita a proposta preliminar gerada pelo modelo de IA:

> ### Proposta de Cenários E2E para o Crypto Alert
> 
> **Cenário 1: Visualização da listagem inicial**
> - *Passos:* Abrir o app, aguardar carregar, verificar se a lista de criptomoedas é exibida com moedas como Bitcoin e Ethereum.
> - *YAML sugerido:*
>   ```yaml
>   appId: host.exp.exponent
>   ---
>   - launchApp
>   - assertVisible: "Cryptocurrencies"
>   - assertVisible: "Bitcoin"
>   - assertVisible: "Ethereum"
>   ```
> 
> **Cenário 2: Conversão de valores**
> - *Passos:* Navegar para a aba "Convert", tocar no campo de valor com placeholder "0.00", digitar "1", fechar teclado e verificar o resultado.
> - *YAML sugerido:*
>   ```yaml
>   appId: host.exp.exponent
>   ---
>   - launchApp
>   - tapOn: "Convert"
>   - assertVisible: "Convert Crypto"
>   - tapOn:
>       placeholder: "0.00"
>   - inputText: "1"
>   - hideKeyboard
>   - assertVisible: "Converted Amount"
>   ```
> 
> **Cenário 3: Criação de alerta de preço**
> - *Passos:* Navegar até "Alerts", clicar no botão de novo alerta, preencher o preço alvo, selecionar condição e salvar.
> - *YAML sugerido:*
>   ```yaml
>   appId: host.exp.exponent
>   ---
>   - launchApp
>   - tapOn: "Alerts"
>   - tapOn: "New Alert"
>   - tapOn:
>       placeholder: "0.00"
>   - inputText: "70000"
>   - tapOn: "Save Alert"
>   - assertVisible: "70,000.00"
>   ```
> 
> **Cenário 4: Navegação entre as abas**
> - *Passos:* Clicar em cada item da TabBar inferior e confirmar a renderização do título da tela correspondente.
> - *YAML sugerido:*
>   ```yaml
>   appId: host.exp.exponent
>   ---
>   - launchApp
>   - tapOn: "Convert"
>   - tapOn: "Alerts"
>   - tapOn: "List"
>   ```
> 
> **Cenário 5: Exclusão de alerta de preço**
> - *Passos:* Na lista de alertas, tocar no ícone de lixeira do primeiro card e validar remoção.
> - *Cenário 6: Validação de erro de campo vazio*
> - *Passos:* Tentar salvar alerta com campo de preço vazio e checar se o botão permanece desabilitado.

---

## 3. Cenários Selecionados

Para a entrega dos quatro fluxos E2E independentes exigidos pela atividade, foram selecionados os cenários mais representativos do ciclo de vida da aplicação:

1. **Fluxo 1 — Listagem de Criptomoedas (`01-crypto-list.yaml`):**  
   Valida o estado inicial, o título principal `"Cryptocurrencies"` e a presença dos símbolos e nomes das moedas principais (`Bitcoin`, `BTC`, `Ethereum`, `ETH`).
2. **Fluxo 2 — Tela de Conversão (`02-crypto-conversion.yaml`):**  
   Valida a navegação para a aba "Convert", os rótulos de campos (`Amount`, `Cryptocurrency`, `Fiat Currency`), a digitação de montante e o cálculo do campo `"Converted Amount"`.
3. **Fluxo 3 — Gestão de Alertas de Preço (`03-price-alerts.yaml`):**  
   Valida o acesso à tela de alertas, navegação para a tela de criação (`Create Alert`), inserção de meta de preço em USD, persistência do registro e validação do valor formatado (`70,000.00`) na listagem retornada.
4. **Fluxo 4 — Navegação entre Funcionalidades (`04-navigation.yaml`):**  
   Valida a integridade do menu inferior (`List` ➔ `Convert` ➔ `Alerts` ➔ `List`) assegurando a transição correta de telas e estados.

---

## 4. Análise Crítica

A comparação entre a proposta inicial da IA generativa e a implementação real no aplicativo revelou pontos cruciais que exigiram intervenção humana:

### O que foi aproveitado:
- **Estrutura dos fluxos principais:** A identificação dos 4 grandes pilares do app (Lista, Conversão, Alertas e Navegação) foi precisa e seguiu a jornada do usuário.
- **Asserções de texto visível:** Uso de textos estáticos como ancoras de asserção (`assertVisible`), aproveitando o suporte nativo do Maestro a elementos acessíveis sem necessidade de IDs artificiais.

### O que foi corrigido:
- **Correção da propriedade inválida `placeholder`:** A IA sugeriu originalmente a propriedade `placeholder: "0.00"` dentro do comando `tapOn:`. No entanto, na especificação do **Maestro CLI 2.12.1**, `placeholder` é uma propriedade não reconhecida (`Unknown Property: placeholder`), provocando falha de parsing do YAML. A intervenção humana corrigiu a sintaxe para a forma canônica suportada pelo Maestro:
  ```yaml
  # Incorreto (sugerido pela IA):
  - tapOn:
      placeholder: "0.00"

  # Correto (validado na revisão humana):
  - tapOn: "0.00"
  ```
- **Fechamento explícito de teclado virtual:** O Maestro pode ter cliques bloqueados se o teclado virtual do Android cobrir botões como o `"Save Alert"` ou mascarar elementos da tela. Adicionou-se o comando `- hideKeyboard` logo após os inputs numéricos nos fluxos 02 e 03.
- **Formatação de valores na asserção:** A IA inicialmente supôs que o valor digitado (`70000`) apareceria bruto na lista. A análise do componente `AlertCard.tsx` revelou a função `formatPrice(alert.targetPrice)`, exigindo que o assert esperasse o valor formatado com separador de milhar: `"70,000.00"`.

### O que foi descartado:
- **Cenário de Exclusão Direta:** Foi descartado da suíte principal de 4 fluxos devido à necessidade de garantir a total **independência entre os testes**. Como o AsyncStorage persiste os dados localmente no dispositivo, a exclusão imediata poderia introduzir efeitos colaterais caso a ordem de execução dos testes variasse.
- **Seletores baseados em coordenadas/pontos (`point`):** Qualquer sugestão de clique por coordenada percentual foi sumariamente rejeitada por tornar os testes instáveis e dependentes de resolução de tela específica.
