
<script setup>
import {ref} from "vue"
import ComponentFooter from "./components/ComponentFooter.vue";
import ComponentHeader from "./components/ComponentHeader.vue"
import ComponentHero from "./components/ComponentHero.vue";
import ComponentBooks from "./components/ComponentBooks.vue";
import ComponentCart from "./components/ComponentCart.vue";
const showCart = ref(false)
const exibirCart = () => {
  showCart.value ? showCart.value = false : showCart.value = true; 
};
function decrementBookToCart(book) {
  const existingBook = cart.value.items.find((item) => item.id === book.id);
  if (existingBook.quantity === 1) {
    cart.value.items = cart.value.items.filter((item) => item.id !== book.id);
  } else {
    existingBook.quantity--;
  }
  cart.value.total -= book.price;
}

function incrementBookToCart(book) {
  const existingBook = cart.value.items.find((item) => item.id === book.id);
  existingBook.quantity++;
  cart.value.total += book.price;
}

function addToCart(book) {
  const existingBook = cart.value.items.find((item) => item.id === book.id);

  if (existingBook) {
    existingBook.quantity++;
  } else {
    cart.value.items.push({ ...book, quantity: 1 });
  }
  cart.value.total += book.price;
  alert(`Adicionado ${book.title} ao carrinho!`);
}


const cart = ref({
  items: [],
  total: 0,
});
const books = [
  {
    id: 1,
    title: 'Comigo na livraria',
    cover: '/covers/comigo-na-livraria.png',
    price: 23.24,
    author: 'Martha Medeiros',
  },
  {
    id: 2,
    title: 'Quincas Borba',
    cover: '/covers/quincas-borba.png',
    price: 23.24,
    author: 'Machado de Assis',
  },
  {
    id: 3,
    title: 'A livraria',
    cover: '/covers/a-livraria.png',
    price: 13.94,
    author: 'Penelope Fitzgerald',
  },
  {
    id: 4,
    title: 'A hora da estrela',
    cover: '/covers/a-hora-da-estrela.png',
    price: 16.84,
    author: 'Clarice Lispector',
  },
  {
    id: 5,
    title: 'O alienista',
    cover: '/covers/o-alienista.png',
    price: 266.92,
    author: 'Machado de Assis',
  },
  {
    id: 6,
    title: 'Mar morto',
    cover: '/covers/mar-morto.png',
    price: 13.95,
    author: 'Jorge Amado',
  },
  {
    id: 7,
    title: 'Grande sertão',
    cover: '/covers/grande-sertao-veredas.png',
    price: 26.04,
    author: 'Guimarães Rosa',
  },
  {
    id: 8,
    title: 'Flor de poemas',
    cover: '/covers/flor-de-poema.png',
    price: 15.81,
    author: 'Cecília Meireles',
  },
];



</script>

<template>
  <ComponentHeader @update-show-cart="exibirCart" />
   <main v-if="showCart">
    <ComponentCart
    :cart="cart"
    @increment-to-cart="incrementBookToCart"
    @decrement-to-cart="decrementBookToCart"
/>

</main>
<main v-else>
  <ComponentHero/>
  <ComponentBooks :books="books" @-add-to-cart="addToCart"/>
  
</main>
<ComponentFooter/>
</template>
<style scoped>


button {
  background-color: #27ae60;
  color: #fff;
  border: none;
  padding: 15px 20px;
  border-radius: 5px;
  font-size: 1rem;
  cursor: pointer;
  gap: 20px;
  display: flex;
  justify-content: center;

  &.outlined {
    background-color: transparent;
    color: #27ae60;
    border: 2px solid #27ae60;
  }

  &.plain {
    background-color: transparent;
    color: black;
    border: none;
    cursor: pointer;
  }
}
.featured {
  display: flex;
  padding: 3vh 8vw;
  border-bottom: 2px solid #27ae6099;

  & div {
    display: flex;
    align-items: center;
    flex: 1;
    justify-content: center;
    gap: 10px;

    & span {
      font-size: 2rem;
    }

    & h2 {
      font-size: 1.2rem;
      font-weight: 700;
    }
  }

  & article:nth-child(2) {
    border-left: 1px solid #27ae6099;
    border-right: 1px solid #27ae6099;
  }
}
</style>
