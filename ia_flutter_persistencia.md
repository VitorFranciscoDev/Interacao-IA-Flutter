# Quando devo usar SharedPreferences em vez de outras opções de persistência de dados?

Você deve usar o `SharedPreferences` **quando precisa armazenar dados simples, pequenos e não sensíveis**, que devem **persistir entre sessões do aplicativo**. Aqui estão os **principais cenários ideais**:

---

## ✅ **Use SharedPreferences quando:**

### 🔹 1. **Salvar preferências e configurações do usuário**

- Tema claro/escuro  
- Idioma selecionado  
- Volume ou brilho  
- Layout preferido

> Exemplo: `prefs.setBool('modo_escuro', true);`

---

### 🔹 2. **Persistir flags booleanas**

- "Primeira vez que abre o app"  
- "Usuário completou tutorial"  
- "Mostrar pop-up de aviso novamente?"

> Exemplo: `prefs.getBool('tutorial_concluido') ?? false;`

---

### 🔹 3. **Salvar pequenos dados de sessão**

- Token de login temporário (não sensível)  
- Última aba ou tela acessada  
- Status de login (ex: `isLoggedIn = true`)

> ⚠️ *Evite guardar senhas ou tokens sensíveis aqui.*

---

### 🔹 4. **Armazenar pequenos caches simples**

- Último ID acessado  
- Nome do usuário exibido no cabeçalho  
- Número de vezes que algo foi feito (ex: visitas)

---

## ❌ **Evite SharedPreferences quando:**

| Situação                                                                  | Melhor Alternativa                                     |
| ------------------------------------------------------------------------- | ------------------------------------------------------ |
| Armazenar listas grandes, objetos complexos, ou dados relacionais         | `Hive`, `Isar`, `SQFLite`                              |
| Armazenar dados sensíveis como tokens, senhas, chaves privadas            | `flutter_secure_storage`                               |
| Precisa de reatividade (atualizar UI automaticamente quando o dado mudar) | `Provider`, `Riverpod`, `Hive` com observação          |
| Precisa fazer consultas complexas (filtros, joins, ordenações)            | `SQFLite`, `Isar`                                      |
| Dados devem ser criptografados e seguros                                  | `flutter_secure_storage`, `EncryptedSharedPreferences` |

---

## 🟨 Em resumo:

| Critério                        | SharedPreferences | Quando usar                                |
| ------------------------------- | ----------------- | ------------------------------------------ |
| Simples, pequeno, chave-valor   | ✅                 | Configurações, flags, sessões              |
| Persistência após fechar o app  | ✅                 | Sim                                        |
| Dados sensíveis ou criptografia | ❌                 | Use `flutter_secure_storage`               |
| Objetos complexos               | ❌                 | Use `Hive`, `Isar` ou `json + SharedPrefs` |
| Reatividade e observabilidade   | ❌                 | Use `Provider`, `Riverpod`, etc.           |

---

Se você quiser, posso montar uma tabela comparativa entre `SharedPreferences`, `Hive`, `Isar`, e `flutter_secure_storage` para seu projeto. Quer?

> //Observações: Como o SharedPreferences foi pouco explicado, decidi ir atrás de saber o que evitar quando for utilizá-lo, e como contornar essas situações.

---

# Como posso lidar com erros ao usar SharedPreferences?

Lidar com erros ao usar `SharedPreferences` no Flutter é importante para garantir que seu app **não trave** ou se comporte de forma inesperada em dispositivos com problemas de armazenamento ou permissões.

Aqui estão **formas práticas e seguras** de tratar erros com `SharedPreferences`:

---

## ✅ **1. Sempre use `try-catch` ao acessar o SharedPreferences**

```dart
import 'package:shared_preferences/shared_preferences.dart';

Future<void> salvarValor(String chave, String valor) async {
  try {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setString(chave, valor);
  } catch (e) {
    print('Erro ao salvar no SharedPreferences: $e');
    // Exibir mensagem, logar, ou usar um fallback
  }
}
````

---

## ✅ **2. Verifique se os dados existem antes de ler**

```dart
Future<String?> carregarValor(String chave) async {
  try {
    final prefs = await SharedPreferences.getInstance();
    if (prefs.containsKey(chave)) {
      return prefs.getString(chave);
    } else {
      return null; // ou um valor padrão
    }
  } catch (e) {
    print('Erro ao ler do SharedPreferences: $e');
    return null;
  }
}
```

---

## ✅ **3. Use valores padrão como fallback**

Evita erros caso o valor não esteja presente ou ocorra uma falha:

```dart
final nome = prefs.getString('nome_usuario') ?? 'Convidado';
```

---

## ✅ **4. Cuidado com conversões de tipo**

```dart
final valor = prefs.get('alguma_chave');
if (valor is String) {
  print('Valor: $valor');
} else {
  print('Tipo inesperado');
}
```

---

## ✅ **5. Trate exceções específicas em plataformas diferentes (Android/iOS)**

```dart
try {
  final prefs = await SharedPreferences.getInstance();
  await prefs.setInt('contador', 1);
} on Exception catch (e) {
  // Pode ser PlatformException, IOException, etc.
  print('Erro: $e');
}
```

---

## ✅ **6. Teste em emuladores e dispositivos reais**

Teste em dispositivos com:

* Pouco armazenamento
* Modos de economia de bateria ativados
* Versões antigas do Android

---

## ✅ **7. Se usar JSON como `String`, valide antes de decodificar**

```dart
import 'dart:convert';

final jsonString = prefs.getString('perfil');
if (jsonString != null) {
  try {
    final Map<String, dynamic> json = jsonDecode(jsonString);
    // use json
  } catch (e) {
    print('Erro ao decodificar JSON: $e');
  }
}
```

---

## ✅ **Resumo das boas práticas**

| Prática                           | Motivo                     |
| --------------------------------- | -------------------------- |
| `try-catch` em toda operação      | Evita travamentos          |
| Verificar `containsKey()`         | Evita `null` inesperado    |
| Usar valores padrão (`??`)        | Garante fallback           |
| Validar tipos                     | Previne erros de tipo      |
| Testar em diferentes dispositivos | Cobertura real de uso      |
| Validar JSON                      | Evita crash ao decodificar |

---

Se quiser, posso montar um exemplo completo de um helper ou service para encapsular o uso do `SharedPreferences` com tratamento de erro. Deseja isso?

> //Observações: Como eu havia dito, SharedPreferences foi pouco explicado, então achei interessante ir atrás de como evitar alguns possíveis erros durante a programação.