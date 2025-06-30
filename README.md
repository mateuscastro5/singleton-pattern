# 🧠 Projeto: Padrão de Projeto - Singleton

## 📌 O que é o padrão Singleton?

O padrão **Singleton** garante que uma classe tenha **apenas uma instância** e fornece um ponto global de acesso a ela.

É muito usado quando você precisa **controlar recursos compartilhados**, como conexões com banco de dados, arquivos de configuração, logs, etc.

---

## 🧱 Estrutura do Singleton

No geral, um Singleton tem:
- Um construtor **privado**
- Um campo estático que guarda a **única instância**
- Um método público estático que retorna essa instância (ex: `getInstance()`)

---

## 💡 Exemplo de uso comum (TypeScript)

Imagine um sistema onde precisamos de uma única instância para gerenciar logs.

### ❌ Exemplo Sem Singleton

```ts
class LoggerSemSingleton {
  log(mensagem: string) {
    console.log(`[LOG - ${new Date().toISOString()}]: ${mensagem}`);
  }
}

// Criação de múltiplas instâncias (não controlado)
const loggerA = new LoggerSemSingleton();
const loggerB = new LoggerSemSingleton();

loggerA.log("Mensagem A");
loggerB.log("Mensagem B");
```

Problemas:
- Instâncias múltiplas criadas
- Falta de centralização e consistência

---

### ✅ Exemplo Com Singleton

```ts
class Logger {
  private static instancia: Logger;

  private constructor() {} // Impede new Logger()

  public static getInstance(): Logger {
    if (!Logger.instancia) {
      Logger.instancia = new Logger();
    }
    return Logger.instancia;
  }

  public log(mensagem: string): void {
    console.log(`[LOG - ${new Date().toISOString()}]: ${mensagem}`);
  }
}

// Uso correto: sempre a mesma instância
const logger1 = Logger.getInstance();
const logger2 = Logger.getInstance();

logger1.log("Primeira mensagem");
logger2.log("Segunda mensagem");

console.log("Mesma instância?", logger1 === logger2); // true
```

---

## ⚖️ Comparativo: Sem Singleton vs Com Singleton

### ❌ Sem Singleton:
- Múltiplas instâncias da classe
- Consumo de memória desnecessário
- Falta de controle (ex: múltiplos loggers, múltiplas conexões)

### ✅ Com Singleton:
- Apenas uma instância
- Centralização e controle
- Menor uso de recursos
- Mais previsível

---

## ✅ Pontos Fortes
- Controla a criação de instâncias
- Facilita o gerenciamento de recursos globais
- Simples de implementar

---

## ❌ Pontos Fracos
- Pode ser considerado um **antipattern** se usado em excesso
- Dificulta testes unitários (acoplamento alto)
- Pode causar problemas em aplicações **multithread** se não for thread-safe (em linguagens como Java ou C++)

---

## 🔚 Conclusão

O Singleton é útil quando precisamos de **controle total sobre uma instância única**, mas deve ser usado com **cautela**. Em sistemas grandes, pode virar um "acesso global disfarçado", criando acoplamento indesejado.

---

## 📽️ Apresentação do Projeto

- [Inserir aqui o link para o vídeo da apresentação no YouTube ou Google Drive]

---

## 💻 Códigos no Repositório

Todos os exemplos estão incluídos neste README por fins didáticos. Para rodar localmente:

```bash
ts-node singleton.ts
```

---

## 📚 Referências

- [Refactoring Guru - Singleton](https://refactoring.guru/pt-br/design-patterns/singleton)
- GoF - Design Patterns: Elements of Reusable Object-Oriented Software
