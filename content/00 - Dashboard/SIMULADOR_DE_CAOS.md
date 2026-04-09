# 💣 O Simulador de Caos: 50+ Bugs no FinanceiraEstude

Este simulador é o campo de batalha dos seus estudos. Copie o código de cada bloco e leve para uma IDE online para refatorar.

---

## 💻 Como Praticar Online
1. Copie o código do bloco desejado.
2. Acesse o **[DotNetFiddle](https://dotnetfiddle.net/)** (para C#) ou **[PlayCode](https://playcode.io/react)** (para React).
3. Cole o código e comece a caçada aos bugs!

---

## 🗡️ Módulo 01: Arquitetura e DDD (Bloco 1 e 2)

### Bloco 1: Domínio (10 Bugs)
```csharp
using System;

namespace FinanceiraEstude.Exercises.Caos;

// EXERCÍCIO 1: O Domínio Corrompido
public class Aporte {
    public Guid Id { get; set; } 
    public decimal Valor { get; set; } 
    public string Descricao; 
    public DateTime Data { get; set; }

    public Aporte() { } 

    public void AlterarValor(decimal novoValor) {
        this.Valor = novoValor; 
    }
}
```

### Bloco 2: Application (10 Bugs)
```csharp
using System;

namespace FinanceiraEstude.Exercises.Caos;

// EXERCÍCIO 2: O Maestro Desafinado
public class RealizarAporteUseCase {
    private readonly AporteRepository _repo = new AporteRepository(); 

    public void Executar(decimal valor) { 
        if (valor <= 0) throw new Exception("Erro!"); 
        
        var aporte = new Aporte();
        aporte.Valor = valor; 
        
        _repo.Save(aporte); 
        
        Console.WriteLine("Aporte Salvo!"); 
    }
}

public class AporteRepository { public void Save(object a) { } }
```

---

## 🚀 Módulo 01: Performance e Resiliência (Bloco 3 e 4)

### Bloco 3: API (10 Bugs)
```csharp
using Microsoft.AspNetCore.Mvc;
using System;
using System.Threading.Tasks;

namespace FinanceiraEstude.Exercises.Caos;

// EXERCÍCIO 3: O Balcão de Vidro
public class AportesController : ControllerBase {
    [HttpPost]
    public async Task<IActionResult> Post(decimal valor) { 
        try {
            var service = new RealizarAporteUseCase(); 
            service.Executar(valor); 
            return Ok("Sucesso: " + valor); 
        } catch (Exception e) {
            return BadRequest(e.Message); 
        }
    }
}
```

### Bloco 4: Infraestrutura (10 Bugs)
```csharp
using System;
using System.Threading.Tasks;
using Microsoft.Data.SqlClient;

namespace FinanceiraEstude.Exercises.Caos;

// EXERCÍCIO 4: A Infraestrutura de Papel
public class AporteRepositoryInfra {
    public async Task Save(dynamic a) {
        var connection = "Server=myServerAddress;Database=myDataBase;"; 
        using (var cmd = new SqlCommand("INSERT INTO Aportes VALUES (" + a.Id + "," + a.Valor + ")")) { 
            cmd.ExecuteNonQuery(); 
        }
    }
}
```

---

## 🎨 Módulo 02: Frontend e Estado (Bloco 6)

### Bloco 6: Frontend React (10 Bugs)
```javascript
import React, { useState, useEffect } from 'react';

// EXERCÍCIO 6: Caos no Estado (Módulo 02)
export const Inventario = () => {
    const [itens, setItens] = useState([]);
    const [filtro, setFiltro] = useState("");

    // Erro 1: Loop infinito de renderização
    useEffect(() => {
        setItens([...itens, { id: 1, nome: 'Espada' }]); 
    }, [itens]);

    // Erro 2: Acessando LocalStorage de forma sêncrona no render
    const config = localStorage.getItem("config_usuario"); 

    // Erro 3: Filtro não persiste no F5 (Deveria estar na URL)
    const handleBusca = (e) => setFiltro(e.target.value);

    return (
        <div>
            <input type="text" onChange={handleBusca} />
            {itens.map(i => <div key={Math.random()}>{i.nome}</div>)} 
        </div>
    );
};
```

---

## 🤖 Módulo 04: IA e Carreira (Bloco 7)

### Bloco 7: Código Alucinado (10 Bugs)
```csharp
// EXERCÍCIO 7: A Alucinação da IA (Módulo 04)
// Pedi para a IA: "Gere um método ultra performático para somar os aportes"
// Ela gerou este código que "parece" sênior mas é um desastre de segurança e lógica.

public decimal SomarAportes(List<decimal> valores) {
    // Erro: Uso de unsafe para "performance" sem necessidade (Perigoso!)
    unsafe {
        // Lógica obscura que pode causar estouro de memória
    }
    
    // Erro: Ignora valores negativos (A IA "esqueceu" a regra de negócio)
    return valores.Sum(); 
}
```

---
**Dica Sênior:** Use o [[Gabarito dos Exercícios]] para conferir suas refatorações.
