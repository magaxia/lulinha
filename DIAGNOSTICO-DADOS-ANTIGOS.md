# 🔧 DIAGNÓSTICO: Dados Antigos em Perfil e Equipe

## ⚠️ PROBLEMA IDENTIFICADO

"equipe e perfil esta puxando dados antigos q nen existe mais"

## 🎯 SOLUÇÃO IMPLEMENTADA

✅ **perfil.html** - Atualizado para:

- Buscar dados ATUALIZADOS do Firestore ao carregar página
- Usar `onSnapshot()` para manter saldo sincronizado em tempo real
- Detectar quando volta para a aba e revalidar dados

✅ **equipe.html** - Atualizado para:

- Forçar recarga de dados REAIS do Firestore ao login
- Adicionar logs detalhados para diagnosticar problemas nas queries
- Melhor tratamento quando coleção "comissoes" está vazia

## 📋 PRÓXIMAS ETAPAS PARA VALIDAÇÃO

### 1️⃣ Abrir Diagnóstico

Abra o arquivo `diagnostico-firestore.html` no navegador:

```
file:///C:/Users/Kalebi/Downloads/Original/diagnostico-firestore.html
```

### 2️⃣ Execute os testes em ordem:

1. **"1️⃣ Testar Autenticação"**
   - Deve mostrar seus dados de login
2. **"2️⃣ Testar Coleção Comissões"**
   - Verificará se a coleção "comissoes" existe
   - Testará diferentes nomes de campo: `usuarioId`, `uid`, `userId`
   - Se uma encontrar dados, anote qual campo está correto
3. **"3️⃣ Testar Coleção Indicações"**
   - Verificará se a coleção "indicacoes" existe
   - Testará busca por `idIndicador`
4. **"4️⃣ Testar Usuário Atual"**
   - Mostrará os dados atuais do seu usuário no Firestore

### 3️⃣ Reporte os Resultados

**Se houver ERRO em "Coleção Comissões":**

- Acesse [Firestore Console](https://console.firebase.google.com)
- Verifique se a coleção "comissoes" realmente existe
- Cheque qual é o nome do campo que contém o UID do usuário

**Se a coleção "comissoes" estiver VAZIA:**

- Isso é normal! Significa: "Você não tem comissões ainda"
- A página agora mostrará: R$ 0,00 com aviso no console

**Se houver ERRO em "Coleção Indicações":**

- Verifique se você realmente adicionou indicações ao sistema
- Cheque se o campo é realmente chamado "idIndicador"

## 🔄 MUDANÇAS FEITAS

### perfil.html

```javascript
// ANTES: Dados do login (ANTIGOS)
document.getElementById("nome").innerText = dadosUsuario.nome || "Usuário";

// DEPOIS: Buscar ATUAIS do Firestore
window.SistemaAuth.db.collection("users").doc(uid).get();
```

### equipe.html

```javascript
// Agora com logs detalhados:
console.log("📊 Documentos encontrados:", snapshot.size);
console.log("💰 Comissão encontrada:", doc.data());
```

## 🆘 Se ainda estiver vendo dados antigos

1. Abra DevTools (F12)
2. Vá para "Application" → "Storage" → "Local Storage"
3. Procure por "usuarioLogado"
4. **Deleta a entrada** (clique direito → Delete)
5. Recarregue a página (Ctrl+F5)

## ✅ CHECKLIST FINAL

- [ ] Teste o diagnóstico-firestore.html
- [ ] Verifique se os dados aparecem corretos
- [ ] Tente entrar em "perfil.html" - deve mostrar dados ATUAIS
- [ ] Tente entrar em "equipe.html" - deve mostrar dados REAIS
- [ ] Se houver problema em comissões, me avise o resultado do teste
- [ ] Se trocar para outra aba e voltar, dados devem se refrescar

---

**Próxima ação:** Execute os testes acima e me reporte os resultados do console!
