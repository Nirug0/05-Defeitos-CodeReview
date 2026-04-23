# 🔎 Formulário — Parte B

> Preencha uma seção por finding. O mínimo esperado é **6 findings**.

**Dupla:** Nicolas Ruiz Gonçalves 
**Data da revisão:** 22/04/2026

---

### Finding #1

**📍 Linha(s):** 12-13
**🏷 Rótulo:** blocker 
**📂 Dimensão:** Segurança
**⚠️ Severidade:** Crítica 

**🐛 Problema:** SQL Injection. O valor da variável nome é concatenado diretamente na string da consulta SQL. Isso permite que um atacante manipule a query para extrair dados sensíveis ou destruir o banco.

**💡 Sugestão de correção:** Utilize parâmetros vinculados (prepared statements) para que o driver do banco de dados trate o dado como texto, não como comando.

```javascript
// ajuste sugerido
async function buscarUsuarioPorNome(nome) {
  const query = "SELECT * FROM usuarios WHERE nome = ?";
  return db.executarQuery(query, [nome]);
}
```

**📚 Referência (opcional):**

---

### Finding #2

**📍 Linha(s):** 16-32
**🏷 Rótulo:** major
**📂 Dimensão:** Erros / Padrões
**⚠️ Severidade:** Alta

**🐛 Problema:** Falta de Validação de Domínio. A constante TIPOS_VALIDOS está declarada mas não é utilizada. O sistema permite cadastrar usuários com tipos inexistentes, o que causará falhas silenciosas nas funções de cálculo de limite.

**💡 Sugestão de correção:** Verifique se o tipo fornecido é válido antes de prosseguir com o cadastro.

```javascript
// ajuste sugerido
async function cadastrarUsuario(dados) {
  if (!TIPOS_VALIDOS.includes(dados.tipo)) {
    throw new Error('Tipo de usuário inválido');
  }
  // ... resto do código
}
```

---

### Finding #3

**📍 Linha(s):** 7, 11, 16, 36 (Funções Async)
**🏷 Rótulo:** major
**📂 Dimensão:** Erros
**⚠️ Severidade:** Alta

**🐛 Problema:** Ausência de Tratamento de Exceções. As funções assíncronas não possuem blocos try/catch. Se o banco de dados falhar ou houver erro na criptografia, a aplicação terá uma "Unhandled Promise Rejection", podendo derrubar o processo Node.js.

**💡 Sugestão de correção:** Envolva as operações críticas em blocos de tratamento de erro.

```javascript
// ajuste sugerido
async function listarUsuariosAtivos() {
  try {
    return await db.executarQuery('SELECT * FROM usuarios WHERE ativo = 1');
  } catch (error) {
    logger.error('Erro ao listar usuários: ' + error.message);
    throw error;
  }
}
```

---

### Finding #4

**📍 Linha(s):** 36-42
**🏷 Rótulo:** major
**📂 Dimensão:** Erros / Padrões
**⚠️ Severidade:** Média

**🐛 Problema:** Update Não Atômico (Race Condition). A função busca o objeto inteiro, altera um campo localmente e salva o objeto todo de volta. Se outro campo for alterado simultaneamente por outro processo, essa alteração será perdida.

**💡 Sugestão de correção:**

```javascript
// ajuste sugerido
async function atualizarEmail(id, novoEmail) {
  await db.executarQuery('UPDATE usuarios SET email = ? WHERE id = ?', [novoEmail, id]);
  logger.info('Email atualizado: ' + novoEmail);
}
```

---

### Finding #5

**📍 Linha(s):** 45-103
**🏷 Rótulo:** Major
**📂 Dimensão:** Complexibilidade / Legibilidade
**⚠️ Severidade:** Média

**🐛 Problema:** Alta Complexidade Ciclomática. O uso de if/else aninhados profundamente (o famoso "Código Pirâmide") torna o teste unitário quase impossível e a leitura extremamente cansativa.

**💡 Sugestão de correção:** Utilize a técnica de Guard Clauses (cláusulas de guarda) para retornar cedo ou separe a lógica por tipo de usuário.

```javascript
// ajuste sugerido
function calcularLimiteEmprestimo(usuario) {
  if (usuario.bloqueadoAte && new Date(usuario.bloqueadoAte) > new Date()) return 0;
  if (usuario.tipo === 'professor') return calcularLimiteProfessor(usuario);
  if (usuario.tipo === 'aluno') return calcularLimiteAluno(usuario);
  return 5; // Limite padrão
}
```

---

### Finding #6

**📍 Linha(s):** 105-141
**🏷 Rótulo:** nit
**📂 Dimensão:** Padrões (DRY)
**⚠️ Severidade:** Baixa

**🐛 Problema:** Código Duplicado. A função calcularLimiteComSuspensao repete 90% da lógica de calcularLimiteEmprestimo. Isso fere o princípio DRY (Don't Repeat Yourself) e gera dívida técnica.

**💡 Sugestão de correção:** Unifique as funções. A verificação de suspensão deve ser apenas uma regra adicional dentro da função principal de cálculo.

```javascript
// ajuste sugerido
// Remova a função duplicada e adicione no início da principal:
if (usuario.suspenso) return 0;
```

---

## ✅ Checklist final

- [ ] Há pelo menos 6 findings preenchidas
- [ ] Cada finding cita linha, dimensão, rótulo e severidade
- [ ] As sugestões são concretas e acionáveis
- [ ] Pelo menos uma finding cobre segurança
- [ ] Pelo menos uma finding cobre complexidade
