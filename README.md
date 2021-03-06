# Web Motion 1.0

> Diretrizes de criação e desenvolvimento de interfaces na Web.

Grandes empresas, que possuem seus produtos multi plataforma, criam produtos diferentes em cada um, isso por causa das limitações e da forma padrão como cada uma funciona. Esse projeto visa explorar todos os recursos da web, para que reduzir suas limitações e criar um padrão.

## Não existe

Um elemento flutuante em qualquer lugar da tela se transportar até um lugar específico e passar a ser fixo. Na Web existe apenas o position sticky, que funciona dentro de uma rolagem e quano chega no limite do elemento em que ele é relativo passa a ser flutuate, porém o elemento não fica em qualquer lugar da ela, nem é transportado até um lugar específico.

O conteúdo de um elemento virar outro. Essas transformações mostradas no Material Design que um botão vira um menu ou uma nova tela não existe. Na Web teria que ser feito uma troca do conteúdo e de alguma forma disfarçar essa transição.

## Proibido

Permitir parar pela metade uma animação de um conteúdo a ser lido.

Uso excessivo do [will-change](https://developer.mozilla.org/pt-BR/docs/Web/CSS/will-change) como solução para o uso de propriedades que recalculam a página, como `padding`, `top`, `left`... Pois além de não resolver deixa a página mais pesada e com mais uso de memória.

## Duração

- Elementos pequenos: 100-200ms
- Transição de página: 500-700ms
- Distância: 100ms para cada 10% da tela
- Complexidade 2-5 elementos: 300-400ms
- Complexidade 6-10 elementos: 500-700ms
- Tamanho da tela\*

**IBM Carbon**

```css
:root {
  --duration--fast-01: 70ms; /* Micro-interactions such as button and toggle */
  --duration--fast-02: 110ms; /* Micro-interactions such as fade */
  --duration--moderate-01: 150ms; /* Micro-interactions, small expansion, short distance movements */
  --duration--moderate-02: 240ms; /* Expansion, system communication, toast */
  --duration--slow-01: 400ms; /* Large expansion, important system notifications */
  --duration--slow-02: 700ms; /* Background dimming */
}
```

**Material Design**

```css
:root {
  --duration-open: 250ms; /* or expand */
  --duration-close: 200ms; /* or collapse */
  --duration-open-large: 300ms; /* or expand large */
  --duration-close-large: 250ms; /* or collapse large */
  --duration-switch: 100ms;
}
```

### Expressivo X Produtivo

Menos de 200ms é produtivo, acima disso é expressivo, ou seja, para puxar a atenção do usuário.

### Media queries

Quanto menor a tela, menos espaço para percorrer. Exceção o PC que na Web o normal é não ter animações, então se forem lentas dão a sensação que o computador está ruim.

- Vestíveis: 150-200ms
- Celular: 200-300ms
- Tablet: 400-450ms
- PC: 150-200ms

## Curvas

Deixam os movimetos mais naturais aos nossos olhos.

A curva padrão é quando um elemento está visível do começo ao fim da animação, ou quando sai da tela e tem a possibilidade de voltar

A curva de entrada é de desaceleração e é usado quando o elemento aparece na tela e de saída, de aceleração, quando sai da tela e nunca mais volta.

**IBM Carbon**

```css
:root {
  --easing-standard-productive: cubic-bezier(0.2, 0, 0.38, 0.9);
  --easing-standard-expressive: cubic-bezier(0.4, 0.14, 0.3, 1);

  --easing-entrance-productive: cubic-bezier(0, 0, 0.38, 0.9); /* ease-out */
  --easing-entrance-expressive: cubic-bezier(0, 0, 0.3, 1); /* ease-out */

  --easing-exit-productive: cubic-bezier(0.2, 0, 1, 0.9); /* ease-in */
  --easing-exit-expressive: cubic-bezier(0.4, 0.14, 1, 1); /* ease-in */
}
```

**Material Design**

```css
:root {
  --easing-standard: cubic-bezier(0.4, 0, 0.2, 1);
  --easing-desacelerated: cubic-bezier(0, 0, 0.2, 1); /* ease-out */
  --easing-accelerated: cubic-bezier(0.4, 0, 1, 1); /* ease-in */
}
```

## Camadas

As camadas são elementos que podem ser sobrepostos e ainda manter a área de toque das camadas anteriores.

![image](https://user-images.githubusercontent.com/27368585/126732419-b6891926-28d3-4f60-943b-11bda47e66f9.png)

### Gatilhos em camadas

Quando uma está se posicionando na tela, é possível criar uns gatilhos baseados em sua posição. O conceito de [Scrollspy](https://github.com/jomarcardoso/ovos/tree/master/src/interface/scroll-spy) pode ser usado aqui.

## Painéis

Painéis são elementos que ocupam a tela toda.

### Painéis de rolagem

Exemplo Instagram

### Painéis de rolagem com paralaxe

### Painéis de sobreposição

Feito com sticky com left ou top 0.

## Placeholders

## Animações de entrada e saída

A coreografia deve ter uma direção natural, sem zigue zague, ou seja, se eslementos tornarem-se visíveis, precisa ser em linha, essa pode ser diagonal.

### Coexistência proibida

Quando um está em tela o outro deixa de existir.

### No mesmo eixo

Para não mostrar o conteúdo se formando pode-se usar um loader e renderizar o conteúdo, após isso fazer o efeito de fade com um translate em todos os elementos.

Referências:

- https://material.io/design/motion/the-motion-system.html#shared-axis

Animação em 300ms

Opção de mesmo eixo.

```css
@keyframes shared-axis-out {
  0% {
    opacity: 1;
  }
  15% {
    transform: translateX(0);
  }
  30% {
    opacity: 0;
  }
  100% {
    transform: translateX(30dp);
  }
}

@keyframes shared-axis-in {
  0% {
    opacity: 0;
  }
  15% {
    transform: translateX(30dp);
  }
  30% {
    opacity: 0;
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}
```

## Transições

### Transições com relação

A troca do conteúdo ser feita com fade out e fade in. O efeito precisa tanto de opacidade como um efeito de expansão.

## Transformação

No meio da transição, com a opacidade zero trocar o conteúdo.

Evitar mudar o formato da forma, apenas o conteúdo.

### Troca de conteúdo

A troca de conteúdo deve ser feita setando o valor inicial e final do container. O valor inicial é o conteúdo atual e o final é o conteúdo que irá aparecer no local, para saber esse tamanho precisa pré renderizar e manter escondido esse conteúdo.

## Tokens

Componentes:

- drawer
- action

## Outros

- Animações com svg
- Angular animations

## Referências

- https://angular.io/guide/animations
- https://material.io/design/motion/understanding-motion.html#principles
- https://material.io/design/shape/shape-motion.html#morphing-shape
- https://www.carbondesignsystem.com/guidelines/motion/overview/
- https://ibm.github.io/motion/
- https://www.designsystems.com/5-steps-for-including-motion-design-in-your-system/
- https://uxdesign.cc/the-ultimate-guide-to-proper-use-of-animation-in-ux-10bd98614fa9
- https://medium.com/design-ibm/working-together-ux-motion-specs-for-design-and-development-249b12d60909
- https://hackernoon.com/using-animationmotion-design-tokens-for-more-complex-and-sophisticated-design-zy3t33y5
- https://easings.net/
