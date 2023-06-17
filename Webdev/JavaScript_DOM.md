# JavaScript DOM

## Identifying HTML elements
`document.querySelector('button'); // finds the first occuring button in the document`

`document.querySelector('.my-btn'); // finds the first occuring "my-btn" class`

### Finding elements by ID
`document.querySelector('#btn-1'); // finds the element with id "btn-1"`

`document.getElementById('btn-1');`

## Adding Elements
```
const newElement = document.createElement('p');
newElement.textContent = "Hello";
document.body.appendChild(newElement);
```

## Listening to Events
```
const btn = document.querySelector('#btn-1'); // identifying the button
// creating the function to append an image to the HTML
function addImg() {
    const newImg = document.createElement('img');
    newImg.src = 'img.png';
    document.body.appendChild(newImg);
}
```
**`btn.addEventListener('click', addImg); // the event listener`**

or it can be done this way: **`btn.onclick = addImg;`**

or like this, in the HTML file: **`button id="btn-1" class="my-btn" onclick="addImg()"></button>`**
