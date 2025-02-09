<template>
    <div class="main-page">
        <div class="nav-bar">
            <h1>
                <span>Mac</span>
                <div>Lanches</div>
            </h1>
            <button @click="openModal">
                Carrinho ({{ cart.length }})
            </button>
        </div>

        <div v-if="isModalOpen" class="modal">
            <div class="modal-content">
                <h2>Carrinho de Compras</h2>
                <div v-if="cart.length === 0">
                    <p>Seu carrinho está vazio!</p>
                </div>
                <div v-else>
                    <ul>
                        <li v-for="(item, index) in cart" :key="index">
                            <div class="cart-item">
                                <img :src="item.image" :alt="item.name" class="cart-item-image" />
                                <div class="cart-item-info">
                                    <span>{{ item.name }}</span>
                                    <span>{{ item.price }}</span>
                                </div>
                            </div>
                        </li>
                    </ul>
                    <div class="total">Total: {{ totalPrice }}</div>
                    <button class="checkout-btn">Finalizar Compra</button>
                </div>
                <button @click="closeModal" class="close-btn">Fechar</button>
            </div>
        </div>

        <div class="products">
            <div class="sales">
                <div class="card" v-for="(product, index) in products" :key="index">
                    <img :src="product.image" :alt="product.name" />
                    <div class="product-title">{{ product.name }}</div>
                    <div class="product-price">{{ product.price }}</div>
                    <button class="order-btn" @click="orderLanche(product)">Comprar</button>
                </div>
            </div>
            <div class="new-product">
                <div class="big-card" v-for="(combo, index) in combos" :key="index">
                    <img :src="combo.image" alt="Combo" />
                    <div class="product-info">
                        <h1>{{ combo.title }}</h1>
                        <h2 class="product-title">{{ combo.name }}</h2>
                        <span class="combo-price">{{ combo.price }}</span>
                        <button class="order-btn" @click="orderLanche(combo)">Comprar</button>
                    </div>
                </div>
            </div>
            <div class="footer">
                <p>&copy; 2025 Mac Lanches - Todos os direitos reservados</p>
                <div class="social-icons">
                    <a href="https://www.facebook.com" target="_blank">Facebook</a>
                    <a href="https://www.instagram.com" target="_blank">Instagram</a>
                    <a href="https://www.twitter.com" target="_blank">Twitter</a>
                </div>
            </div>

        </div>
    </div>
</template>

<script>
export default {
    name: 'MainPage',
    data() {
        return {
            products: [
                {
                    name: "Lanche Muito Bom 1",
                    price: "R$20,99",
                    image: "https://images2.nogueirense.com.br/wp-content/uploads/2023/10/captura-de-tela-173-1697742218-e1697742355907.png"
                },
                {
                    name: "Lanche Muito Bom 2",
                    price: "R$24,99",
                    image: "https://images2.nogueirense.com.br/wp-content/uploads/2023/10/captura-de-tela-177-1697742247-e1697742567256.png"
                },
                {
                    name: "Três Lanches Muito Bons",
                    price: "R$44,99",
                    image: "https://offloadmedia.feverup.com/saopaulosecreto.com/wp-content/uploads/2021/05/29044255/miha-rekar-ISVtBKNhJ2g-unsplash-1024x819.jpg"
                }
            ],
            combos: [
                {
                    title: "COMBO!!!",
                    name: "Lanche Bonzinho + Coca 350Ml e Fritas!",
                    price: "R$21,99",
                    image: "https://mirassolconectada.com.br/wp-content/uploads/2019/02/WhatsApp-Image-2019-02-27-at-ds.jpg"
                },
                {
                    title: "Promoção do rolê",
                    name: "4 Lanches + Batata grande",
                    price: "R$51,99",
                    image: "https://guiadohamburguer.com/wp-content/uploads/2020/09/10-sliders-dez-hamburguerias-940x959.jpg"
                }
            ],
            cart: [],
            isModalOpen: false
        };
    },
    computed: {
        totalPrice() {
            return this.cart.reduce((acc, item) => {
                const price = parseFloat(item.price.replace('R$', '').replace(',', '.'));
                return acc + price;
            }, 0).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
        }
    },
    methods: {
        orderLanche(item) {
            this.cart.push(item);
        },
        openModal() {
            this.isModalOpen = true;
            this.$nextTick(() => {
                document.querySelector('.modal').classList.add('open');
            });
        },
        closeModal() {
            this.isModalOpen = false;
            document.querySelector('.modal').classList.remove('open');
        }
    }
};

</script>
  <style scoped>
  .main-page {
      font-family: Verdana, Geneva, Tahoma, sans-serif;
  }
  
  .nav-bar {
      background-color: white;
      padding: 10px 20px;
      border-radius: 8px;
      border-bottom: rgba(152, 152, 152, 0.355) solid;
      display: flex;
      justify-content: space-between;
      align-items: center;
  }
  
  .nav-bar h1 {
      margin: 0;
      display: flex;
      align-items: center;
  }
  
  .nav-bar>h1>span {
      color: red;
      font-size: 1.8rem;
      margin-right: 5px;
  }
  
  .nav-bar>h1>div {
      color: #e68900;
      font-size: 1.5rem;
  }
  
  button {
      background-color: #ff9800;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1.2rem;
      padding: 10px 20px;
  }
  
  button:hover {
      background-color: #e68900;
  }
  
  .products {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
  }
  
  .sales {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: center;
      padding: 20px;
  }
  
  .card {
      background-color: white;
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 10px;
      width: 200px;
      text-align: center;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      height: 300px;
  }
  
  .big-card {
      display: flex;
      flex-direction: row;
      align-items: center;
      background-color: white;
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 10px;
      width: 690px;
      max-width: 100%;
      text-align: left;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      height: 300px;
  }
  
  .card img,
  .big-card img {
      width: 100%;
      height: 100px;
      object-fit: cover;
      border-radius: 8px;
  }
  
  .big-card img {
      width: 350px;
      height: 250px;
      border-radius: 8px;
      margin-right: 20px;
  }
  
  .product-info {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      height: 100%;
  }
  
  .product-info>h1 {
      text-align: center;
  }
  
  .product-title {
      text-align: center;
      font-size: 1.2rem;
      color: #333;
  }
  
  .product-price {
      font-size: 1.5rem;
      color: #e68900;
      font-weight: 700;
  }
  
  .combo-price {
      text-align: center;
      font-size: 2rem;
      color: #e60000;
      font-weight: 700;
  }
  
  .order-btn {
      background-color: #38e68c;
      margin-top: 20px;
      padding: 8px;
      border-radius: 5px;
      color: white;
      border: none;
      cursor: pointer;
      font-size: 1.1rem;
      transition: background-color 0.3s ease, transform 0.3s ease;
  }
  
  .order-btn:hover {
      background-color: #2cb970;
  }
  
  .footer {
      margin-top: 20px;
      background-color: #f48a00;
      color: white;
      padding: 20px;
      text-align: center;
      position: relative;
      width: 100%;
  }
  
  .footer .social-icons {
      margin-top: 10px;
  }
  
  .footer .social-icons a {
      margin: 0 10px;
      color: white;
      text-decoration: none;
  }
  
  .footer .social-icons a:hover {
      text-decoration: underline;
  }
  
  .modal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 999;
      overflow: hidden;
  }
  
  .modal-content {
      background-color: white;
      padding: 20px;
      border-radius: 8px;
      width: 400px;
      max-width: 100%;
      text-align: center;
  }
  
  .cart-item {
      display: flex;
      align-items: center;
      margin-bottom: 10px;
  }
  
  .cart-item-image {
      width: 50px;
      height: 50px;
      object-fit: cover;
      border-radius: 50%;
      margin-right: 10px;
  }
  
  .cart-item-info {
      display: flex;
      flex-direction: column;
  }
  
  .total {
      margin-top: 20px;
      font-size: 1.5rem;
      font-weight: 700;
  }
  
  .close-btn {
      background-color: rgb(148, 29, 29);
      color: white;
      border: none;
      border-radius: 5px;
      padding: 10px;
      cursor: pointer;
      margin-top: 20px;
  }
  
  .close-btn:hover {
      background-color: darkred;
  }
  
  .checkout-btn {
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      padding: 10px;
      cursor: pointer;
      margin-top: 10px;
  }
  
  .checkout-btn:hover {
      background-color: #45a049;
  }
  </style>
  