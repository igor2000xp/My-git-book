# It-incubator shop  3️⃣Страница с товаром

### 3️⃣Страница с товаром

1\) ⚡Теперь при клике на кнопку **show more** будем переходить на страницу с товаром.

* Для этого нам понадобится библиотека [**react-router**](https://reactrouter.com/), которую мы устанавливали ранее

2\) ⚡Первым шагом обернем наше приложение `BrowserRouter`

```typescript
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import { BrowserRouter } from "react-router";
import App from "./App.tsx";

createRoot(document.getElementById("root")!).render(
  <BrowserRouter>
    <StrictMode>
      <App />
    </StrictMode>
  </BrowserRouter>,
);
```

3\) ⚡Если в url пустой слеш, тогда отрисуем `BestSellers`

```typescript
import "./App.css";
import { Route, Routes } from "react-router";
import { BestSellers } from "./BestSellers.tsx";
import { Header } from "./Header.tsx";

function App() {
  return (
    <div className="appContainer">
      <Header />
      <Routes>
        <Route path="/" element={<BestSellers />} />
      </Routes>
    </div>
  );
}
export default App;
```

4\) ⚡Создадим компонент **Product**. В tsx в качестве заглушки напишем **\<h1>Product\</h1>**

```typescript
export const Product = () => {
  return (
    <div>
      <h1>Product</h1>
    </div>
  );
};
```

5\) ⚡Если в url будет адрес `/product`, тогда отрисуем `Product`

```typescript
function App() {
  return (
    <div className="appContainer">
      <Header />
      <Routes>
        <Route path="/" element={<BestSellers />} />
        <Route path="/product" element={<Product />} />
      </Routes>
    </div>
  );
}
```

Теперь в урле давайте руками будем менять роутинг ( **/** или **product**) и видеть как отрисовываются разные страницы 💪

6\) ⚡Теперь на странице товара сделаем по аналогии еще один запрос на сервер для получения одного товара и положим его тоже в стейт

```typescript
import axios from "axios";
import { useEffect, useState } from "react";
import type { Product as ProductType } from "./BestSellers.tsx";

export const Product = () => {
  const [product, setProduct] = useState<ProductType | null>(null);

  useEffect(() => {
    axios
      .get("https://masterclass.kimitsu.it-incubator.io/api/products/1")
      .then((res) => {
        const product = res.data;
        setProduct(product);
      });
  }, []);

  return (
    <div>
      <h1>Product</h1>
    </div>
  );
};
```

7\)⚡ Теперь отрисуем полученную информацию о товаре с сервера

Чтобы не тратить время на верстку держите код

```typescript
import axios from "axios";
import { useEffect, useState } from "react";
import type { Product as ProductType } from "./BestSellers.tsx";
import rating from "./assets/img/rating.svg";
import cartWhite from "./assets/img/cartWhite.svg";

export const Product = () => {
  const [product, setProduct] = useState<ProductType | null>(null);

  useEffect(() => {
    axios
      .get("https://masterclass.kimitsu.it-incubator.io/api/products/8")
      .then((res) => setProduct(res.data));
  }, []);

  if (product === null) {
    return <h2>Продукт еще грузится ...</h2>;
  }

  return (
    <div>
      <div>Заглушка. Понадобится чуть позже. Не удаляйте :)</div>

      <div className="product">
        <img src={product.image} alt="" />
        <div className="info">
          <p className="title">{product.title}</p>
          <p className="price">$ {product.price}</p>
          <div className="rating">
            <p>Rating: {product.rating.rate}</p>
            <img src={rating} alt="" />
          </div>
          <div className="category">
            <span>Category:</span>
            <p>{product.category}</p>
          </div>
          <p className="description">{product.description}</p>
          <button>
            <img src={cartWhite} alt="" />
            Add to cart
          </button>
        </div>
      </div>
    </div>
  );
};
```

8\)⚡ Если все сделали правильно, то должны получить следующий результат 💪

<div align="left"><img src="https://safronman.gitbook.io/react-intro-lesson/~gitbook/image?url=https%3A%2F%2F79070263-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FhTGeEIgJENaO5jIZvlrS%252Fuploads%252F1U3yOomaiqoSBt11j1Jj%252Fzip-hoodie.png%3Falt%3Dmedia%26token%3D03b9af79-e7ae-4f7a-9569-3f7ee91a74fb&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=8e973dc3&#x26;sv=2" alt="" width="563"></div>

