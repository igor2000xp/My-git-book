# It-incubator shop - 4️⃣Роутинг

### 4️⃣Роутинг

1\) ⚡Теперь при клике на кнопку show more будем переходить на страницу с товаром.

Но на самом деле show more это не кнопка, а **ссылка**, потому что она ведет на новый адрес.

Для того чтобы работать со ссылками нам понадобится компонент [**Link** ](https://reactrouter.com/start/library/navigating#link)из **react-router**

```typescript
<Link to={'/product'}>Show more</Link>
```

Для того чтобы ссылка выглядела как кнопка, добавим ей соответствующие стили

```css
.card a {
  background-color: white;
  border: 1px solid #2068F8;
  border-radius: 2px;
  padding: 10px 0;
  width: 80%;
  color: #2068F8;
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  align-self: center;
  margin-bottom: 36px;
  cursor: pointer;
  text-align: center;
  text-decoration: none;
}
```

Обратите внимание, что при наведении на show more мы видим адрес на который мы перейдем

![](https://safronman.gitbook.io/react-intro-lesson/~gitbook/image?url=https%3A%2F%2F79070263-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FhTGeEIgJENaO5jIZvlrS%252Fuploads%252FXsiwVkdV7y5LFGb6Tpkg%252Fimg-link-2.png%3Falt%3Dmedia%26token%3D91483bcc-52ec-4788-a53d-71c2eacb1542\&width=768\&dpr=4\&quality=100\&sign=4933d96d\&sv=2)

Попробуйте нажать на show more. После этого шага можно переходить со страницы бестселлеров на страницу продукта 🚀

2\) ⚡Кликая на продукт мы всегда получаем один и тот же товар. Почему? 🤔

Открываем network и смотрим. Мы делаем запрос за одним и тем же товаром, а нужно за разными. Как же это реализовать?🤔 Смотрим на Id. Руками меняем id и видим как меняется результат. Как же при клике сказать компоненту чтобы он подгружал товар с нужным id ? 🤔

3\) ⚡Для того чтобы получить ответ на предыдущий вопрос нужно ознакомиться с еще одним хуком из библиотеки react-router-dom. Встречайте [**useParams**](https://reactrouter.com/start/library/url-values#route-params)

```typescript
function App() {
  return (
    <div className="appContainer">
      <Header />
      <Routes>
        <Route path="/" element={<BestSellers />} />
        <Route path="/product/:productId" element={<Product />} />
      </Routes>
    </div>
  );
}
```

```typescript
export const Product = () => {
  const [product, setProduct] = useState<ProductType | null>(null);

  const { productId } = useParams();

  useEffect(() => {
    axios
      .get(
        `https://masterclass.kimitsu.it-incubator.io/api/products/${productId}`,
      )
      .then((res) => setProduct(res.data));
  }, []);

 /*...*/
};
```

Теперь давайте поставим debugger в **Product.jsx.** Руками меняем id в url и видим разные товары 💪

4\) ⚡Все, что осталось сделать это использовать этот **uri параметр в url**. Идем в компонент **Bestellers.jsx** и изменяем адрес ссылки

```typescript
export const BestSellers = () => {
  /*...*/
  return (
    <div className="bestSeller">
      <h2>Bestsellers</h2>
      <div className="cards">
        {products.map((pr) => {
          return (
            <div className="card">
              <img src={pr.image} alt="img" />
              <h4>{pr.title}</h4>
              <p className="price">${pr.price}</p>
              <Link to={`/product/${pr.id}`}>Show more</Link>
            </div>
          );
        })}
      </div>
    </div>
  );
};
```

И после этого кликаем по товарам и видим каждый раз нужный вариант 🚀

![](https://safronman.gitbook.io/react-intro-lesson/~gitbook/image?url=https%3A%2F%2F79070263-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FhTGeEIgJENaO5jIZvlrS%252Fuploads%252FyXZFJvaZOgfmwatPulne%252FAnimation.gif%3Falt%3Dmedia%26token%3Dc2f24bb3-eaa5-47ad-81e8-bb0c389e4444\&width=768\&dpr=4\&quality=100\&sign=e03eca2\&sv=2)

5\) ⚡Теперь давайте реализуем чтобы при нажатии на стрелочку назад, возвращаться на главную страницу.

Но для начал отрисуем разметку и поправим стили

```typescript
import axios from "axios";
import { useEffect, useState } from "react";
import { Link, useParams } from "react-router";
import type { Product as ProductType } from "./BestSellers.tsx";
import rating from "./assets/img/rating.svg";
import cartWhite from "./assets/img/cartWhite.svg";
import arrowBack from "./assets/img/arrowBack.svg";

export const Product = () => {
 /*... */

  return (
    <>
      <div className="arrowBack">
        <Link to={"/"}>
          <img src={arrowBack} alt="arrowBack" />
          Back to Best Seller
        </Link>
      </div>

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
    </>
  );
};
```

Теперь мы можем с со страницы товара вернуться на главную страницу. **Это победа** 🚀

Last updated 6 months ago
