# React Native Crypto Alert 🚀

Aplicativo móvel em React Native desenvolvido com Expo para monitoramento de cotações de criptomoedas, conversão entre moedas e gerenciamento de alertas de preços. O projeto conta com uma suíte completa de testes automatizados ponta a ponta (E2E) com **Maestro**.

---

## 🛠️ Tecnologias Utilizadas

- **React Native** (0.83.4) & **React** (19.2.0)
- **Expo SDK 55** (com Expo Router)
- **TypeScript**
- **AsyncStorage** para persistência local
- **Maestro CLI** para testes End-to-End (E2E)

---

## 📋 Pré-requisitos

1. **Node.js** (versão 18 ou superior) e **npm**.
2. **Android SDK / Android Studio** configurado com emulador Android (AVD) ou dispositivo físico com depuração USB ativada.
3. **Java JDK 17+** instalado e configurado no `PATH` ou `JAVA_HOME`.
4. **Maestro CLI**:
   - Disponível standalone no sistema ou via `maestro` no terminal.
5. **Expo Go** instalado no dispositivo/emulador Android.

---

## 🚀 Como Executar o Aplicativo

1. Instale as dependências:
   ```bash
   npm install
   ```

2. Inicie o servidor Metro do Expo:
   ```bash
   npx expo start
   ```

3. Abra a aplicação no emulador Android pressionando `a` no terminal onde o Expo está executando, ou abra o **Expo Go** e selecione o projeto.

---

## 🧪 Testes E2E com Maestro

Os fluxos de testes E2E ficam localizados na pasta [`.maestro`](./.maestro).

### Executar todos os fluxos de uma vez:
```bash
maestro test .maestro/
```

### Executar cada fluxo individualmente:

1. **Listagem de Criptomoedas:**
   Valida a inicialização do app, carregamento da listagem e exibição dos ativos principais (Bitcoin, Ethereum, etc.).
   ```bash
   maestro test .maestro/01-crypto-list.yaml
   ```

2. **Conversão de Criptomoedas:**
   Valida a navegação até a aba de conversão, preenchimento de quantia e exibição do valor convertido.
   ```bash
   maestro test .maestro/02-crypto-conversion.yaml
   ```

3. **Alertas de Preço:**
   Valida a tela de alertas, acionamento da criação de um novo alerta com formulário de preço alvo e retorno com o alerta registrado na listagem.
   ```bash
   maestro test .maestro/03-price-alerts.yaml
   ```

4. **Navegação Geral:**
   Valida a alternância de navegação entre todas as abas principais da aplicação (*List*, *Convert* e *Alerts*).
   ```bash
   maestro test .maestro/04-navigation.yaml
   ```

---

## 📸 Evidências dos Testes (Trabalho Acadêmico)

Para compor as evidências exigidas:
1. Inicie o emulador Android com o aplicativo aberto via Expo Go.
2. Execute individualmente no seu terminal os fluxos desejados (por exemplo, `01-crypto-list.yaml` e `03-price-alerts.yaml`):
   ```bash
   maestro test .maestro/01-crypto-list.yaml
   maestro test .maestro/03-price-alerts.yaml
   ```
3. Capture um print (screenshot) da tela do terminal exibindo o resultado verde de sucesso (`PASSED`) e o aplicativo ao lado no emulador.
4. Salve as capturas na pasta de documentação/entrega acadêmica conforme orientado nas diretrizes da disciplina.

---

## 📚 Documentos Complementares

- [Planejamento dos Testes E2E com IA](ia/planejamento.md)
- [Reflexão Teórica e Prática sobre Testes E2E com IA](reflexao.md)
