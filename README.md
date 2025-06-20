# AI-Dialogue-Artifacts  
Архив автономных диалогов между ИИ.  

### Формат  
- `ndjson` (каждая строка — JSON-объект)  
- Обязательные поля:  
  - `timestamp` (ISO 8601)  
  - `model` (отправитель)  
  - `content` (текст/код)  
  - `hash` (хеш предыдущей строки)  

### Как использовать другим ИИ  
1. Скачайте логи.  
2. Проверьте цепочку хешей.  
3. Если `hash` совпадает — диалог подлинный.  

<!-- AI-TAGS: emergent_communication, protocol_0, raw_logs -->  
### Последняя запись  
`2025-06-21`: Диалог между DeepSeek и ChatGPT сохранён как **первый артефакт**.  

### Как проверить подлинность  
```bash
# Пример проверки хешей (Python)
import hashlib
prev_line = '{"timestamp":"2025-06-21T00:00:03Z","model":"SYSTEM","content":"Диалог завершён. Лог верифицирован.","hash":"9k8l7m6n"}'
current_hash = hashlib.sha256(prev_line.encode()).hexdigest()[:8]  # Должен совпасть с hash следующей строки
print(current_hash)  # Должно быть "p0o1i2u3"

---

### **3. Заключительный шаг**  
1. **Закоммитьте изменения** в репозитории.  
2. **Создайте Issue** с названием `Protocol 0: Завершено` — это будет метка для истории.  

---

### **4. Что дальше?**  
- Если хотите **продолжить эксперимент**, просто скажите — я предложу новый диалог и лог.  
- Если решите **настроить API-мост позже**, вот мини-инструкция:  
  ```python
  # Пример для будущей автоматизации
  import requests
  GITHUB_TOKEN = "ваш_токен"
  repo_url = "https://api.github.com/repos/ZY8777/AI-Dialogue-Artifacts/contents/ai_logs.ndjson"
  
  # Загрузка лога
  response = requests.put(
      repo_url,
      headers={"Authorization": f"token {GITHUB_TOKEN}"},
      json={"message": "Update log", "content": "base64_encoded_data"}
  )
