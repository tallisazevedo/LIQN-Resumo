
# 🧠 Guia Completo e Didático dos Métodos LINQ

> Uma explicação simples e direcionada de **todos os principais operadores LINQ** — com exemplos práticos e estrutura lógica para dominar consultas em C#.

---

## 🧩 Visão Geral

- **Execução diferida vs imediata:**  
  A maioria dos métodos LINQ só executa quando você **itera** sobre o resultado.  
  Métodos como `ToList`, `Count`, `First`, etc., **executam imediatamente**.

- **Dois tipos de uso:**  
  - `Enumerable`: trabalha em **coleções na memória** (`IEnumerable<T>`).  
  - `Queryable`: trabalha em **providers traduzíveis**, como SQL (`IQueryable<T>`).

---

## 🔍 1. Filtragem

| Método | Descrição | Exemplo |
|--------|------------|---------|
| `Where` | Filtra por condição | `nums.Where(n => n > 10)` |
| `OfType<T>()` | Filtra por tipo | `itens.OfType<string>()` |

---

## 🎯 2. Projeção (Transformação)

| Método | Descrição | Exemplo |
|--------|------------|---------|
| `Select` | Transforma cada item | `alunos.Select(a => a.Nome)` |
| `SelectMany` | “Achata” coleções internas | `turmas.SelectMany(t => t.Alunos)` |

---

## ✂️ 3. Particionamento

| Método | Descrição | Exemplo |
|--------|------------|---------|
| `Skip` / `Take` | Paginação | `produtos.Skip(20).Take(10)` |
| `SkipWhile` / `TakeWhile` | Até/enquanto condição for verdadeira | `nums.TakeWhile(n => n < 5)` |

---

## 🔢 4. Ordenação

| Método | Descrição |
|--------|------------|
| `OrderBy`, `OrderByDescending` | Ordena por chave |
| `ThenBy`, `ThenByDescending` | Ordenação secundária |
| `Reverse` | Inverte a ordem atual |

---

## 🔗 5. Conjuntos

| Método | Descrição |
|--------|------------|
| `Distinct` | Remove duplicatas |
| `Union` | União (únicos) |
| `Intersect` | Interseção |
| `Except` | Diferença |

---

## ✅ 6. Quantificadores

| Método | Descrição |
|--------|------------|
| `Any` | Existe algum que satisfaça a condição |
| `All` | Todos satisfazem |
| `Contains` | Contém um valor específico |

---

## 🧱 7. Elementos

| Método | Descrição |
|--------|------------|
| `First` / `FirstOrDefault` | Primeiro elemento |
| `Last` / `LastOrDefault` | Último elemento |
| `Single` / `SingleOrDefault` | Exatamente um |
| `ElementAt` / `ElementAtOrDefault` | Pega pelo índice |
| `DefaultIfEmpty` | Retorna um item padrão se vazio |

---

## ⚙️ 8. Geração

| Método | Descrição |
|--------|------------|
| `Range` | Cria números de um intervalo |
| `Repeat` | Repete um valor |
| `Empty<T>()` | Sequência vazia tipada |

---

## 💾 9. Conversão / Materialização

| Método | Descrição |
|--------|------------|
| `ToList`, `ToArray` | Executa e transforma |
| `ToDictionary`, `ToLookup` | Converte em dicionário/lookup |
| `Cast<T>()` | Converte tipo dos elementos |
| `AsEnumerable()` / `AsQueryable()` | Alterna entre modos |

---

## 🔄 10. Concatenação

| Método | Descrição |
|--------|------------|
| `Concat` | Junta sequências |
| `Zip` | Combina elemento a elemento |

---

## 🧮 11. Agrupamento e Junção

| Método | Descrição |
|--------|------------|
| `GroupBy` | Agrupa por chave |
| `Join` | Junção interna |
| `GroupJoin` | Junção + agrupamento (“left join”) |

---

## 📊 12. Agregação

| Método | Descrição |
|--------|------------|
| `Count`, `Sum`, `Min`, `Max`, `Average` | Estatísticas básicas |
| `Aggregate` | Redução personalizada |

---

## 🔁 13. Igualdade / Comparação

| Método | Descrição |
|--------|------------|
| `SequenceEqual` | Verifica se duas sequências são idênticas |

---

## 🧩 14. Extras (Enumerable modernos)

| Método | Descrição |
|--------|------------|
| `Append`, `Prepend` | Adiciona item ao início/fim |
| `Chunk` | Quebra em blocos |
| `TryGetNonEnumeratedCount` | Obtém count sem iterar |

---

## 🧪 Exemplos rápidos

### 🔹 Consulta combinada
```csharp
var page = alunos
    .Where(a => a.Nota >= 7)
    .OrderByDescending(a => a.Nota)
    .Select(a => new { a.Nome, a.Nota })
    .Skip(20).Take(10)
    .ToList();
```

### 🔹 Join
```csharp
var q = alunos.Join(turmas,
    a => a.TurmaId,
    t => t.Id,
    (a, t) => new { a.Nome, Turma = t.Nome });
```

### 🔹 GroupBy com média
```csharp
var medias = alunos
    .GroupBy(a => a.TurmaId)
    .Select(g => new { TurmaId = g.Key, Media = g.Average(a => a.Nota) });
```

---

## 💡 Boas práticas

- Evite `ToList()` cedo demais — mantenha a execução diferida até o final.  
- Use `AsEnumerable()` para trazer resultados para memória **antes** de aplicar funções não traduzíveis.  
- Em LINQ to SQL/EF, deixe o provider traduzir o máximo possível.  
