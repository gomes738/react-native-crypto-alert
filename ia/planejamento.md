Prompt: Desenvolver trabalho acadêmico de testes E2E com Maestro para React Native Crypto Alert.

Resposta original da IA (planejamento preliminar):
- Analisar estrutura do projeto React Native.
- Identificar telas: Listagem de criptomoedas, Conversão, Alertas, Navegação.
- Mapear componentes e seletores existentes usando Expo Router e React Navigation.
- Definir fluxos E2E com Maestro considerando elementos reais (botões, listas, inputs).
- Preparar documentação e reflexão sobre IA.

Cenários selecionados para testes E2E:
1. Exibir lista de criptomoedas na tela inicial.
2. Realizar conversão de valores entre criptomoedas.
3. Configurar e visualizar alertas de preço.
4. Navegar entre as telas principais usando a barra de navegação.

Análise crítica:
- Necessário validar seletores reais (testID, accessibilityLabel) antes de escrever scripts.
- Verificar se a tela de alertas está implementada; caso não, o teste será adaptado.
- Considerar estado inicial limpo (sem dados persistidos) usando async‑storage reset.
- Avaliar tempo de carregamento dos componentes para definir esperas adequadas no Maestro.
- Garantir que os testes sejam independentes e possam rodar em qualquer ordem.
