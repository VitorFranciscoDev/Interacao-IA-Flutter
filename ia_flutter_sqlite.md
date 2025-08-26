Pergunta: Quais são as vantagens de usar SQLite em aplicativos Flutter?

Usar **SQLite** em aplicativos Flutter oferece várias vantagens, especialmente quando se trata de armazenar dados localmente de forma estruturada e persistente. Aqui estão as principais:

---

### ✅ **1. Armazenamento local persistente**

* Ideal para apps que precisam manter dados mesmo após serem fechados.
* Ex: listas de tarefas, notas, configurações do usuário.

---

### ✅ **2. Estrutura relacional**

* Permite usar **tabelas, chaves primárias, relacionamentos** e **consultas SQL** complexas.
* Útil para modelagem de dados mais rica e estruturada, como num mini banco de dados.

---

### ✅ **3. Offline-first**

* SQLite é local e **não depende de conexão com a internet**.
* Perfeito para apps que funcionam offline e sincronizam depois com um servidor.

---

### ✅ **4. Performance**

* Excelente desempenho para leituras e escritas rápidas em grandes volumes de dados.
* Mais eficiente que armazenar tudo em arquivos ou usando `SharedPreferences` para dados estruturados.

---

### ✅ **5. Suporte maduro e multiplataforma**

* SQLite é **estável e testado** há muitos anos, sendo usado em Android, iOS, Windows, etc.
* Bibliotecas como [`sqflite`](https://pub.dev/packages/sqflite) oferecem suporte fácil para Flutter.

---

### ✅ **6. Controle total sobre o banco**

* Você pode executar **SQL puro**, criar índices, normalizar dados, etc.
* Mais flexibilidade comparado a soluções chave-valor como `SharedPreferences`.

---

### ✅ **7. Baixa dependência externa**

* Não exige serviços externos como Firebase, tornando o app mais leve e independente.

---

## Quando usar SQLite em Flutter?

Use SQLite quando:

* Precisa armazenar **dados complexos estruturados** localmente.
* Precisa fazer **buscas, ordenações ou filtros** com desempenho.
* Quer **armazenar dados offline** com segurança e controle.

---

Se quiser, posso te mostrar um exemplo prático com `sqflite` usando um CRUD completo. Deseja isso?

//Observações: Quando programamos um aplicativo, temos algumas opções de bancos de dados para utilizarmos, então fiquei com dúvida sobre quais seriam as vantagens de utilizar o SQLite ao invés dos outros.