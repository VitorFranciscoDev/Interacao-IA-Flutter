Pergunta: Qual a diferença entre um TextField e um TextFormField?

Em Flutter, tanto `TextField` quanto `TextFormField` são usados para
entrada de texto, mas há **diferenças importantes** entre eles,
principalmente relacionadas à **validação** e **integração com
formulários**.

------------------------------------------------------------------------

### 🔹 `TextField`

-   É o **widget mais básico** para entrada de texto.
-   Não oferece suporte embutido à **validação de formulário**.
-   Ideal para campos simples e independentes, fora de formulários.
-   Pode ser usado com um `TextEditingController` para controlar o
    valor.

``` dart
TextField(
  controller: meuController,
  decoration: InputDecoration(labelText: 'Nome'),
)
```

------------------------------------------------------------------------

### 🔸 `TextFormField`

-   É uma **extensão de `TextField`**, feita para funcionar **dentro de
    um `Form`**.
-   Suporta **validação de formulário** por meio da propriedade
    `validator`.
-   Trabalha diretamente com o método `FormState.validate()` e
    `FormState.save()`.
-   Ideal para uso em formulários completos.

``` dart
Form(
  key: _formKey,
  child: Column(
    children: [
      TextFormField(
        validator: (value) {
          if (value == null || value.isEmpty) {
            return 'Este campo é obrigatório';
          }
          return null;
        },
        decoration: InputDecoration(labelText: 'Nome'),
      ),
    ],
  ),
)
```

------------------------------------------------------------------------

### ✅ Quando usar cada um?

  ------------------------------------------------------------------------
  Situação                                 Use           Use
                                           `TextField`   `TextFormField`
  ---------------------------------------- ------------- -----------------
  Entrada de texto simples, fora de        ✅            ❌
  formulário                                             

  Validação de formulário                  ❌            ✅

  Formulário com múltiplos campos          ❌            ✅

  Sem necessidade de validação             ✅            ✅
  ------------------------------------------------------------------------

------------------------------------------------------------------------

Se estiver usando um `Form` e precisa de **validação automática**, use
`TextFormField`. Se só precisa de um campo de texto básico, `TextField`
já é suficiente.

Se quiser, posso te mostrar um exemplo comparando os dois em um app
Flutter.

//Observações: Fiquei na dúvida sobre essa diferença entre os dois
TextFields, porém consegui entender bem essa diferença com a resposta da
IA.

Pergunta: Como posso alterar a cor e a forma de um CheckBox e de um
Radio?

Em Flutter, tanto `Checkbox` quanto `Radio` têm propriedades que
permitem **personalizar a cor** e **a forma** (no caso do `Checkbox`).
Abaixo explico como fazer isso para cada um:

------------------------------------------------------------------------

## ✅ **Checkbox**

### 🔹 Alterar cor:

Você pode usar as seguintes propriedades:

-   `activeColor`: cor quando **selecionado**
-   `checkColor`: cor do **ícone de check**
-   `fillColor`: cor de fundo do contorno (mais flexível)

``` dart
Checkbox(
  value: true,
  onChanged: (value) {},
  activeColor: Colors.green,     // cor do contorno ativo
  checkColor: Colors.white,      // cor do check
  fillColor: MaterialStateProperty.all(Colors.green), // cor geral (ativa/inativa)
)
```

### 🔸 Alterar forma:

Use a propriedade `shape`:

``` dart
Checkbox(
  value: true,
  onChanged: (value) {},
  shape: RoundedRectangleBorder(   // pode ser circular, arredondado etc.
    borderRadius: BorderRadius.circular(4),
  ),
)
```

------------------------------------------------------------------------

## 🔘 **Radio**

### 🔹 Alterar cor:

-   `activeColor`: cor do botão quando **selecionado**
-   `fillColor`: cor do círculo (pode variar com estados)

``` dart
Radio<int>(
  value: 1,
  groupValue: 1,
  onChanged: (value) {},
  activeColor: Colors.blue, // cor do círculo selecionado
  fillColor: MaterialStateProperty.all(Colors.blueAccent),
)
```

### ❗ Forma do Radio:

O `Radio` **não permite alterar a forma diretamente** (é sempre
circular). Se quiser um botão com forma personalizada, você pode usar
`RadioListTile` ou criar algo customizado com `GestureDetector`.

------------------------------------------------------------------------

## 🔧 Exemplo completo:

``` dart
Column(
  children: [
    Checkbox(
      value: true,
      onChanged: (v) {},
      activeColor: Colors.deepPurple,
      checkColor: Colors.white,
      shape: RoundedRectangleBorder(
        borderRadius: BorderRadius.circular(8),
      ),
    ),
    Radio<int>(
      value: 1,
      groupValue: 1,
      onChanged: (v) {},
      activeColor: Colors.orange,
      fillColor: MaterialStateProperty.all(Colors.orange),
    ),
  ],
)
```

Se quiser, posso te mostrar como criar um `Checkbox` ou `Radio` **com
estilo totalmente customizado** usando `InkWell` + `Container`. Deseja
isso também?

//Observações: Acho importante deixar a interface do aplicativo mais
atrativa por meio dos estilos, cores e etc., e consegui ter uma melhor
noção dos estilos e formas dos dois componentes por meio dessa resposta.
