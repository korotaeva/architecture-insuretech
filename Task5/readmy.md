
Примеры запросов
1. Только основная информация о клиенте
   query GetClientBasic($clientId: ID!) {
       client(id: $clientId) {
           id
           name
           age
       }
   }
2. Клиент + документы (без родственников)
   query GetClientWithDocuments($clientId: ID!) {
       client(id: $clientId, includeDocuments: true) {
           id
           name
           documents {
               id
               type
               number
           }
       }
   }
3. Полный профиль клиента
query GetFullClientProfile($clientId: ID!) {
   client(id: $clientId, includeDocuments: true, includeRelatives: true) {
       id
       name
       age
       documents {
           type
           number
           expiryDate
       }
       relatives {
           name
           relationType
       }
   }
}
Проблема REST	                             Решение в GraphQL
N+1 запросов для связанных данных	        Один запрос с нужными связями (client + documents + relatives)
Фиксированные ответы (over-fetching)	    Клиент выбирает только необходимые поля
Отдельные эндпоинты для каждой сущности	    Единая точка входа с гибким выбором данных
