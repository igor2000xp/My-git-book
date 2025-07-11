# Дом. задание: Вводное занятие по React 2️⃣Добавление в корзину

### 2️⃣Добавление в корзину

1\) ⚡Реализуем добавление в корзину. При нажатии на кнопку "Add to cart" нужно сделать:

* показать alert с надписью "Товар успешно добавлен в корзину"
* поменять имя кнопки на "Go to cart"
* добавить активный стиль для кнопки

Подсказка

```
 import axios from "axios";
import { useEffect, useState } from "react";
import { Link, useParams } from "react-router";
import type { Product as ProductType } from "./BestSellers.tsx";
import rating from "./assets/img/rating.svg";
import cartWhite from "./assets/img/cartWhite.svg";
import cart from "./assets/img/cart.svg";
import arrowBack from "./assets/img/arrowBack.svg";
import { Reviews } from "./Reviews.tsx";

export const Product = () => {
  const [product, setProduct] = useState<ProductType | null>(null);

  const [isProductInCart, setIsProductIncart] = useState<boolean>(false);

  const { productId } = useParams();

  useEffect(() => {
    axios
      .get(
        `https://masterclass.kimitsu.it-incubator.io/api/products/${productId}`,
      )
      .then((res) => setProduct(res.data));
  }, []);

  const addProductToCartHandler = () => {
    alert("Товар успешно добавлен в корзину");
    setIsProductIncart(true);
  };

  if (product === null) {
    return <h2>Продукт еще грузится ...</h2>;
  }

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

          <button
            onClick={addProductToCartHandler}
            className={`button ${isProductInCart ? "active" : ""}`}
          >
            <img src={isProductInCart ? cart : cartWhite} alt="cart icon" />
            {isProductInCart ? "Go to cart" : "Add to cart"}
          </button>
        </div>
      </div>

      <Reviews />
    </>
  );
};

 
```

добавьте новый стиль для кнопки

```
.product .info button.active  {
  background: #ffffff;
  border-radius: 4px;
  width: 100%;
  padding: 14px;
  color: #2068f8;
  border: 2px solid #2068f8 ;
  font-weight: 500;
  font-size: 16px;
  line-height: 20px;
  display: flex;
  justify-content: center;
}
```

**Результат 🚀**

![](https://safronman.gitbook.io/dom.-zadanie-vvodnoe-zanyatie-po-react/~gitbook/image?url=https%3A%2F%2F3220636581-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FAVPdQiALlFxTi9ISP9e6%252Fuploads%252FzoPrL5pSaZn86ZX7YDIO%252FAnimation2.gif%3Falt%3Dmedia%26token%3D4006ab47-0316-4039-9bc6-953c22b66179\&width=768\&dpr=4\&quality=100\&sign=a2bbd2a3\&sv=2)

Last updated 6 months ago
