# Jogo do Número Secreto

## 📌 Sobre o Projeto
Este é um jogo simples onde o jogador tenta adivinhar um número secreto gerado aleatoriamente. O jogo fornece dicas se o número secreto é maior ou menor que o chute do jogador e exibe a quantidade de tentativas ao acertar.

## 🚀 Tecnologias Utilizadas
- HTML
- CSS
- JavaScript

## 📂 Estrutura do Projeto

O projeto é composto pelos seguintes arquivos:

```
📁 jogo-numero-secreto
│── 📄 index.html  # Estrutura da página
│── 📄 style.css   # Estilização da interface
│── 📄 app.js      # Lógica do jogo
│── 📁 img         # Imagens utilizadas no jogo
```

## 🎮 Como Jogar
1. O jogo inicia exibindo uma mensagem para escolher um número entre 1 e 10.
2. O jogador digita um número e clica no botão "Chutar".
3. O jogo fornece uma dica se o número secreto é maior ou menor.
4. Quando o jogador acerta, a quantidade de tentativas é exibida.
5. O botão "Novo Jogo" fica disponível para reiniciar a partida.

## 🔧 Funcionalidades Principais

### 🔢 Geração de Número Secreto
O número secreto é gerado aleatoriamente e não se repete antes de todos os números possíveis serem sorteados:
```javascript
function gerarNumeroAleatorio() {
    let numeroEscolhido = parseInt(Math.random() * numeroLimite + 1);
    if (listaDeNumerosSorteados.includes(numeroEscolhido)) {
        return gerarNumeroAleatorio();
    } else {
        listaDeNumerosSorteados.push(numeroEscolhido);
        return numeroEscolhido;
    }
}
```

### 📢 Exibição de Mensagens
Mensagens dinâmicas são exibidas na tela e podem ser narradas por síntese de voz:
```javascript
function exibirTextoNaTela(tag, texto) {
    let campo = document.querySelector(tag);
    campo.innerHTML = texto;
    if ('speechSynthesis' in window) {
        let utterance = new SpeechSynthesisUtterance(texto);
        utterance.lang = 'pt-BR'; 
        utterance.rate = 1.2; 
        window.speechSynthesis.speak(utterance);
    }
}
```

### 🎯 Verificação do Chute
O jogador recebe um feedback indicando se o número secreto é maior ou menor:
```javascript
function verificarChute() {
    let chute = document.querySelector("input").value;
    if (chute == numeroSecreto) {
        exibirTextoNaTela("h1", "Acertou!");
        exibirTextoNaTela("p", `Você descobriu o número secreto com ${tentativas} tentativas!`);
        document.getElementById("reiniciar").removeAttribute("disabled");
    } else {
        exibirTextoNaTela("p", chute > numeroSecreto ? "O número secreto é menor" : "O número secreto é maior!");
        tentativas++;
        limparCampo();
    }
}
```

### 🔄 Reinício do Jogo
Permite começar uma nova partida com um novo número secreto:
```javascript
function reiniciarJogo() {
    numeroSecreto = gerarNumeroAleatorio();
    limparCampo();
    tentativas = 1;
    exibirMensagemInicial();
    document.getElementById("reiniciar").setAttribute("disabled", true);
}
```

## 🎨 Estilização (CSS)
O design do jogo conta com um fundo gradiente e elementos estilizados para uma interface agradável:
```css
body {
    background: linear-gradient(#1354A5 0%, #041832 33.33%, #041832 66.67%, #01080E 100%);
    display: flex;
    align-items: center;
    justify-content: center;
}
.container {
    width: 80%;
    height: 80%;
    border-radius: 24px;
    border: 1px solid #1875E8;
    box-shadow: 4px 4px 20px 0px rgba(1, 8, 14, 0.15);
}
```

## 📌 Melhorias Futuras
- Adicionar níveis de dificuldade.
- Aumentar o intervalo de números para desafiar mais os jogadores.
- Criar um sistema de pontuação.


