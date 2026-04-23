# 🐛 Bug Reports — Parte A

> Preencha uma seção completa para cada defeito encontrado. O mínimo
> exigido é **3 bug reports**. Apague este bloco antes de entregar.

**Dupla:** Nicolas Ruiz 187222

**Data da exploração:** 22/04/2025

**Navegador usado:** Chrome 121

**Sistema operacional:** Windows 11


---

## BUG-001

**Título:** [LISTA] Número de tarefas aparece como um número maior do que o apresentado.

**Severidade:** Baixa
**Justificativa da severidade:** (É fácil de perceber que o número está somente errado.)

**Prioridade:** P2
**Justificativa da prioridade:** (É possível conviver com o bug, porém chato)

**Ambiente:**
- Navegador: Chrome 121
- Sistema Operacional: Windows 11
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Escrever as informações da tarefa
2. Na opção de "Prioridade", colocar prioridade 5
3. A lista conta a tarefa duas vezes, aparecendo com um número a mais de tarefas

**Resultado esperado:**
Número certo de tarefas.

**Resultado obtido:**
Número errado de tarefas, acima do normal.

**Evidência:**
[Pendentes aparece como "2", sendo que é somente 1.](bug1.png)

> Se preferir anexar um GIF ou arquivo de log, crie uma pasta
> `evidencias/` ao lado deste arquivo e referencie o arquivo aqui.

**Sugestão de causa raiz (opcional):**
É a prioridade 5, porém não sei o motivo.

---

## BUG-002

**Título:** [LISTA] É possível adicionar tarefas com prioridade maior que 5.

**Severidade:** Alta
**Justificativa da severidade:** Eu posso estar buscando por tarefas de prioridade máxima, onde o número "5" fica vermelho, porém a tarefa estaria com um número errado e sem o vermelho de alerta.

**Prioridade:** Média
**Justificativa da prioridade:** Acho dificil selecionar a prioridade errada.

**Ambiente:**
- Navegador: Chrome 121
- Sistema Operacional: Windows 11
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Escrever as informações da tarefa
2. Na opção de "Prioridade", colocar prioridade acima de 5
3. A lista deveria recusar, porém aceita

**Resultado esperado:** Não aceitar a tarefa com prioridade acima de 5.

**Resultado obtido:** Tarefa aceita.

**Evidência:**
[Tarefa aparece como prioridade "10"](bug2.png)

**Sugestão de causa raiz (opcional):**

---

## BUG-003

**Título:** [LISTA] Tarefa pode ser colocada sem prioridade.

**Severidade:** Baixa
**Justificativa da severidade:** Acho quase impossível alguém adicionar uma tarefa sem prioridade

**Prioridade:** Baixa
**Justificativa da prioridade:** Acho quase impossível alguém adicionar uma tarefa sem prioridade

**Ambiente:**
- Navegador: Chrome 121
- Sistema Operacional: Windows 11
- Versão da aplicação: TarefaQS v1.0.00.0

**Passos para reprodução:**
1. Escrever o nome da tarefa
2. Na opção de "Prioridade", não colocar nada
3. A lista deveria recusar, porém aceita, e fica uma tarefa sem prioridade (NaN)
4. 
**Resultado esperado:** Recusar a tarefa sem prioridade.

**Resultado obtido:** Tarefa aceita.

**Evidência:**
[Tarefa aparece como prioridade "NaN"](bug3.png)

**Sugestão de causa raiz (opcional):**

---

<!-- Para reports adicionais, copie o bloco acima trocando o número. -->

---

## ✅ Critérios de qualidade do bug report
*(Use para conferir antes de entregar)*

- [ ] Título descritivo — outra pessoa entende o problema só pelo título?
- [ ] Passos são **numerados** e **reproduzíveis** por terceiros?
- [ ] Há **pelo menos uma evidência** (screenshot, GIF ou log)?
- [ ] Severidade tem **justificativa explícita**?
- [ ] Prioridade tem **justificativa explícita**?
- [ ] Ambiente inclui **navegador + SO**?
- [ ] "Esperado vs. Obtido" deixa o gap claro?

## ✅ Checklist de qualidade dos reports

Antes de submeter, confirme em cada report:

- [ ] Título é específico e acionável (não `"Não funciona"`).
- [ ] Passos estão **numerados** e são reproduzíveis por terceiros.
- [ ] Há **pelo menos uma evidência** por report (imagem, GIF ou log).
- [ ] Severidade tem **justificativa explícita**.
- [ ] Prioridade tem **justificativa explícita**.
- [ ] Ambiente inclui **navegador + SO**.
- [ ] "Esperado × Obtido" deixa a diferença clara.
- [ ] Os 3 defeitos reportados cobrem **categorias diferentes**
      (funcional, UX, validação, persistência, etc.)
