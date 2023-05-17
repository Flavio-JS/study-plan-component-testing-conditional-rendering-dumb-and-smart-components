# Plano de Estudo: Componentes Burros e Inteligentes

## Conceito de "Componente Burro" e "Componente Inteligente"

- Pesquise sobre os conceitos de "Componente Burro" e "Componente Inteligente" na arquitetura de software.

Os conceitos de "Componente Burro" e "Componente Inteligente" referem-se a abordagens diferentes na organização e separação de responsabilidades dos componentes.

Um "Componente Burro" é responsável apenas pela exibição de informações ou interação com o usuário. Ele não possui lógica de negócio complexa e não mantém seu próprio estado. Em vez disso, recebe dados e funcionalidades por meio de props e os renderiza. Um exemplo é um componente de exibição de lista que recebe um array de itens e os renderiza na interface.

Por outro lado, um "Componente Inteligente" é responsável pelo gerenciamento da lógica de negócio e estado do componente. Ele pode conter ações, manipulação de eventos, chamadas de API e lógica complexa. Ao contrário do componente burro, o componente inteligente possui seu próprio estado interno e pode modificá-lo conforme necessário. Ele também pode passar dados e funcionalidades para outros componentes burros por meio de props.

Essa separação entre componentes burros e inteligentes segue o princípio da separação de responsabilidades, tornando o código mais modular, reutilizável e facilitando os testes, uma vez que a lógica de negócio está isolada em componentes específicos.

Ao projetar seus componentes em Next.js, é importante identificar quais componentes são apenas responsáveis pela exibição e quais precisam gerenciar o estado e a lógica. Essa separação ajuda a criar uma estrutura organizada, facilitando a manutenção e extensão do código.

- Compreenda a diferença entre eles, focando na separação da lógica de negócio dos componentes.

A diferença entre um "Componente Burro" e um "Componente Inteligente" está na separação da lógica de negócio dos componentes.

Um "Componente Burro" é responsável apenas pela exibição de informações e interação com o usuário. Ele não possui lógica de negócio complexa e não mantém estado próprio. Recebe dados e funcionalidades por meio de props e os renderiza na interface.

Por outro lado, um "Componente Inteligente" é responsável por gerenciar a lógica de negócio e o estado do componente. Ele contém ações, manipulação de eventos, chamadas de API e lógica mais complexa. Possui seu próprio estado interno e pode modificar e manipular esses dados conforme necessário.

Essa separação é benéfica porque mantém a lógica de negócio isolada em componentes específicos, tornando o código mais modular, reutilizável e facilitando os testes. Os componentes burros focam na exibição e interação, enquanto os componentes inteligentes lidam com a lógica e o estado do componente.

## Exemplos Práticos de Separação entre "Componente Burro" e "Componente Inteligente"

### Exemplo 1: Lista de Itens

**Componente Burro (Dumb Component):**

`Item.js`: Responsável por renderizar um único item da lista. Recebe os dados do item por meio das props e os exibe na interface.

**Componente Inteligente (Smart Component):**

`Lista.js`: Responsável por gerenciar a lógica da lista de itens. Faz a chamada à API para obter os dados dos itens e passa-os para o componente `Item.js` por meio de props.

### Exemplo 2: Formulário de Contato

**Componente Burro (Dumb Component):**

`Input.js`: Responsável por renderizar um campo de entrada de texto. Recebe a propriedade `value` e o manipulador de eventos `onChange` para exibir e atualizar o valor do campo.

**Componente Inteligente (Smart Component):**

`Formulario.js`: Responsável por gerenciar a lógica do formulário de contato. Mantém o estado dos campos de entrada no componente e implementa a lógica de validação e envio do formulário. Passa os valores e manipuladores de eventos para os componentes `Input.js` por meio de props.

Esses são apenas exemplos básicos para ilustrar a separação entre os componentes burros e inteligentes. Em um projeto real, você pode ter uma estrutura de componentes mais complexa, onde os componentes burros são reutilizáveis em várias partes do aplicativo, enquanto os componentes inteligentes lidam com a lógica de negócio específica de cada página ou funcionalidade.

A implementação exata depende do contexto do seu projeto, mas a ideia geral é identificar quais componentes são responsáveis apenas pela exibição e quais precisam gerenciar o estado e a lógica, separando-os adequadamente para obter um código mais organizado e fácil de dar manutenção.

## Testando Condições de Renderização

### Pesquise sobre técnicas de testes de renderização em componentes.

**React Testing Library:**
A biblioteca React Testing Library é amplamente utilizada para testar a renderização de componentes em Next.js. Ela fornece uma série de utilitários e métodos para selecionar elementos da interface, interagir com eles e realizar asserções sobre o que é exibido na tela.

### Explore bibliotecas e frameworks que facilitem o teste de renderização, como Jest, React Testing Library, Enzyme, etc.

#### Instalação das dependências

Certifique-se de ter o Jest, o React Testing Library e as dependências relacionadas instaladas no seu projeto. Você pode instalá-las executando o seguinte comando no terminal, dentro do diretório do seu projeto:

```javascript
npm install --save-dev jest @testing-library/react @testing-library/jest-dom @babel/preset-react ts-jest babel-jest @babel/preset-typescript @babel/preset-env
```

Crie um arquivo `jest.config.js` e adicione o seguinte conteúdo:

```javascript
module.exports = {
  preset: "ts-jest",
  testEnvironment: "jsdom",
  transform: {
    "^.+\\.(ts|tsx)?$": "babel-jest",
  },
};
```

Crie um arquivo `.babelrc` e adicione o seguinte conteúdo:

```javascript
{
  "presets": ["@babel/preset-env", "@babel/preset-react", "@babel/preset-typescript"]
}
```

#### Exemplo

Suponha que temos um componente chamado `ExemploComponente` que renderiza um parágrafo apenas se a propriedade `mostrar` for verdadeira. Caso contrário, não renderiza nada.

```javascript
import React from "react";

interface IExemploComponenteProps {
  mostrar: boolean;
}

const ExemploComponente = ({ mostrar }: IExemploComponenteProps) => {
  return (
    <div>{mostrar && <p>Condição atendida, exibindo o parágrafo!</p>}</div>
  );
};

export { ExemploComponente };
```

Para testar essa condição de renderização usando a biblioteca React Testing Library, podemos escrever o seguinte teste:

```javascript
import React from "react";
import { render, screen } from "@testing-library/react";
import { ExemploComponente } from "./ExemploComponente";
import "@testing-library/jest-dom";

describe("ExemploComponente", () => {
  it("deve renderizar corretamente quando a prop 'mostrar' for verdadeira", () => {
    render(<ExemploComponente mostrar={true} />);

    expect(
      screen.queryByText("Condição atendida, exibindo o parágrafo!")
    ).toBeInTheDocument();
  });

  it("não deve renderizar o parágrafo quando a prop 'mostrar' for falsa", () => {
    render(<ExemploComponente mostrar={false} />);

    expect(
      screen.queryByText("Condição atendida, exibindo o parágrafo!")
    ).toBeNull();
  });
});
```

Neste exemplo, estamos utilizando a função `render` da biblioteca React Testing Library para renderizar o componente `ExemploComponente` com diferentes valores para a propriedade `mostrar`. Em seguida, utilizamos o método `queryByText` para obter referências aos elementos presentes na tela.

Em seguida, realizamos asserções (testes) para verificar se o parágrafo é renderizado corretamente quando a condição é verdadeira e se não é renderizado quando a condição é falsa.

Essa abordagem nos permite testar a lógica de renderização do componente e garantir

## Exemplos Práticos

- Procure por tutoriais e exemplos de código que demonstrem a separação de regras de negócio e os testes de condições de renderização.
- Experimente aplicar esses conceitos em um projeto de estudo ou em um componente real do seu trabalho.
- Discuta suas descobertas e desafios com seus colegas e seu tech lead para obter feedback e orientações adicionais.
