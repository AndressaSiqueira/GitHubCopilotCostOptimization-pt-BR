---
name: free-events-endpoint
description: Use ao criar ou atualizar um endpoint de eventos gratuitos
---

# Endpoint de eventos gratuitos

1. Filtre os eventos em que `price === 0`
2. Filtre os eventos dos próximos 7 dias
3. Exclua registros inválidos ou incompletos
4. Ordene os resultados por data crescente
5. Retorne `{ count, events }`