---
title: Node.textContent
slug: Web/API/Node/textContent
---

{{APIRef("DOM")}}

Позволяет задавать или получать текстовое содержимое элемента и его потомков.

## Синтаксис

```
var text = element.textContent;
element.textContent = "Это просто текст";
```

## Описание

- `textContent` возвращает `null,` _если узел является [документом](/ru/docs/Web/API/Document), типом документа, или его описанием_. Для получения _всего_ текста и CDATA-данных во всём документе можно использовать `document.documentElement.textContent`.
- Если узел является CDATA, комментарием, инструкцией, или текстовым элементом, `textContent` возвращает текст внутри узла в виде строки (т.н. [nodeValue](/ru/docs/Web/API/Node/nodeValue)).
- Для узлов других типов `textContent` возвращает конкатенацию свойств `textContent` всех дочерних узлов, исключая комментарии и строки кода. Если узел не имеет дочерних узлов, будет возвращена пустая строка.
- Установка данного значения удаляет все дочерние узлы и заменяет их единичным текстовым узлом с указанным значением.

### Отличие от `innerText`

`element.innerText` был введён Internet Explorer-ом. Работает по тому же принципу за небольшими исключениями:

- `textContent` получает содержимое _всех_ элементов, включая {{HTMLElement("script")}} и {{HTMLElement("style")}}, тогда как `innerText` этого не делает.
- `innerText` умеет считывать стили и не возвращает содержимое скрытых элементов, тогда как `textContent` этого не делает.
- Метод `innerText` позволяет получить CSS, а `textContent` — нет.

### Отличие от `innerHTML`

`innerHTML`, как можно понять из его названия, возвращает HTML. Довольно часто `innerHTML` используется для получения или записи текста в элемент. Тем не менее, вместо него желательно использовать `textContent`: этот метод потребляет гораздо меньше ресурсов, так как текст парсится как текст, а не HTML. Кроме того, это защищает от XSS атак.

## Пример

```js
// Дан следующий фрагмент:
//   <div id="block">Это — <span>просто</span> текст</div>

// Достаём текстовое содержимое:
var text = document.getElementById("block").textContent;
// В переменной |text| находится: "Это — просто текст".

// Меняем текст:
document.getElementById("block").textContent = "Это — просто текст";
// Теперь наш фрагмент выглядит так:
//   <div id="block">Это — просто текст</div>
```

## Совместимость с браузерами

{{Compat}}

## Спецификации

- [textContent](https://www.w3.org/TR/2004/REC-DOM-Level-3-Core-20040407/core.html#Node3-textContent)

## Смотрите также

- [Подробнее о различиях `innerText` и `textContent`](http://perfectionkills.com/the-poor-misunderstood-innerText/) (пост в блоге)
