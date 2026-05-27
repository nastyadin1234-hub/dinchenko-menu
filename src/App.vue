<script setup>
import { ref, computed } from 'vue'
import ProductCard from './components/ProductCard.vue'
import bannerImg from './assets/banner.jpg'
import eclairsImg from './assets/eclairs.webp'
import milfierImg from './assets/IMG_20260503_153550.webp'
import cakeImg from './assets/IMG_20260503_211046.webp'
import tartImg from './assets/IMG153828.webp'    
import tartCutImg from './assets/IMG154557.webp'
import blackforestImg from './assets/IMG_20260504_154535.webp'
import blackforestcutImg from './assets/IMG_20260504_154550.webp'
import blackforestnewImg from './assets/IMG_20260504_153943 (1).webp'
import blackforestcutnewImg from './assets/IMG_20260504_153948.webp'
import pryanikSetImg from './assets/Screenshot 2026-05-04 175052.jpg'
import pryanikCircleImg from './assets/Screenshot 2026-05-04 175121.jpg'
import pryanikHouseImg from './assets/Screenshot 2026-05-04 175155.jpg'
import pryanikBigImg from './assets/Screenshot 2026-05-04 175208.jpg'
import pryanikCutImg from './assets/Screenshot 2026-05-04 175138.jpg'
import zaherImg from './assets/IMG_20260509_120359 (1).webp'
import zaherCutImg from './assets/IMG_20260504_154047.webp'
import zyzhikImg from './assets/IMG_20260504_154103.webp'
import zyzhikcutImg from './assets/Screenshot 2026-05-12 190038.jpg'
import bombaImg from './assets/IMG_20260504_153904.webp'
import schtollenImg from './assets/IMG_20260504_154230.webp'
const currentCategory = ref('desserts')
const fontSize = ref(18)
const searchQuery = ref('')
const isFormOpen = ref(false)
const initialFormState = () => ({
  title: '',
  price: null,
  category: 'desserts',
  weight: '',
  desc: '',
  badge: ''
})
const newProductData = ref(initialFormState())

const allProducts = ref([
 { 
    id: 1, 
    title: 'Французский «Мильфей»', 
    price: 'По запросу', 
    category: 'desserts', 
    images: [milfierImg], 
    currentImgIndex: 0,
    badge: 'Фирменный рецепт',
    weight: '12*8 см',
    desc: 'Хрустящие коржи из слоеного теста, сливочный крем «Diplomat»'
  },
  { 
    id: 2, 
    title: 'Карамельные Макарон', 
    price: 'По запросу', 
    category: 'desserts', 
    images: [macaronImg, macaroncutImg], 
    currentImgIndex: 0,
    badge: 'Новинка',
    weight: 'набор из 5 шт.',
    desc: 'Выполнен на итальянской меренге, ганаш из карамельного шоколада со сливками, мягкая соленая карамель'
  },
  { 
    id: 3, 
    title: 'Грушевая «Шарлотт»', 
    price: 'По запросу', 
    category: 'desserts', 
    images: [cakeImg], 
    currentImgIndex: 0,
    badge: 'Премиум',
    weight: 'от 1 кг',
    desc: 'Бисквит Савоярди, карамелизованные груши, крем «Bavarois»'
  },
  { 
    id: 4, 
    title: 'Эклеры «New York Cheesecake»', 
    price: 'По запросу', 
    category: 'desserts', 
    images: [eclairsImg, eclairscutImg], 
    currentImgIndex: 0,
    badge: 'Спецпредложение',
    weight: 'набор из 3 шт.',
    desc: 'Безглютеновое тесто, творожно-сливочный крем, клубничное желе'
  },
  { 
    id: 5, 
    title: 'Муссовый торт «Sachertorte»', 
    price: 'По запросу', 
    category: 'desserts', 
    images: [zaherImg, zaherCutImg], 
    currentImgIndex: 0,
    weight: 'от 1 кг',
    desc: 'Шоколадный бисквит, прослойка из абрикосового и мандаринового конфитюра в сочетании с «бобами тонка», шоколадный мусс'
  },
  { 
    id: 6, 
    title: 'Тарталетка с ягодами', 
    price: 'По запросу', 
    category: 'desserts', 
    images: [tartImg, tartCutImg], 
    currentImgIndex: 0,
    weight: '1 шт.',
    desc: 'Песочное тесто, ванильный ганаш, ягодное желе, свежие ягоды'
  },
  { 
    id: 7, 
    title: 'Имбирные пряники', 
    price: 'По запросу', 
    category: 'bakery', 
    images: [pryanikSetImg, pryanikCircleImg, pryanikHouseImg], 
    currentImgIndex: 0,
    weight: '1 шт.',
    desc: 'Ароматное медовое тесто с имбирем и корицей, ручная художественная роспись сахарной глазурью'
  },
  { 
    id: 8, 
    title: 'Печатный пряник с начинкой', 
    price: 'По запросу', 
    category: 'bakery', 
    images: [pryanikBigImg, pryanikCutImg], 
    currentImgIndex: 0,
    weight: '1 шт.',
    desc: 'Традиционное медовое тесто с пряностями, густая начинка из протертой домашней смородины и яблок'
  },
  { 
    id: 9, 
    title: 'Брауни «Irish Stout»', 
    price: 'По запросу', 
    category: 'desserts', 
    images: [bombaImg], 
    currentImgIndex: 0,
    weight: 'от 300 г',
    desc: 'Брауни на пиве Stout с грецким орехом, ванильный ганаш, карамель'  
  },
  { 
    id: 10, 
    title: 'Ванильные профитроли с шоколадным ганашем', 
    price: 'По запросу', 
    category: 'desserts', 
    images: [zyzhikImg, zyzhikcutImg], 
    currentImgIndex: 0,
    weight: 'набор из 5 шт.',
    desc: 'Сливочный крем с натуральной ванилью и насыщенный шоколадный ганаш'
  },
  { 
    id: 11, 
    title: 'Классический «Черный лес»', 
    price: 'По запросу', 
    category: 'desserts', 
    images: [blackforestImg, blackforestcutImg], 
    currentImgIndex: 0,
    weight: 'от 1 кг',
    desc: 'Шоколадный бисквит, сливочный и шоколадный ганаш, вишневое желе'
  },
  { 
    id: 12, 
    title: 'Рождественский штоллен', 
    price: 'По запросу', 
    category: 'bakery', 
    images: [schtollenImg], 
    currentImgIndex: 0,
    weight: '500 г',
    desc: 'Творожное тесто, цукаты на роме Barceló, масло Нуазетт'
  },
  { 
    id: 13, 
    title: 'Черный лес «Modern»', 
    price: 'По запросу', 
    category: 'desserts', 
    images: [blackforestnewImg, blackforestcutnewImg], 
    currentImgIndex: 0,
    weight: 'от 1 кг',
    desc: 'Шоколадный бисквит, вишневое желе, нежный сливочный мусс'
  }
])

const filteredProducts = computed(() => {
  return allProducts.value.filter(product => {
    const matchesCategory = currentCategory.value === 'all' || product.category === currentCategory.value
    const matchesSearch = product.title.toLowerCase().includes(searchQuery.value.toLowerCase())
    return matchesCategory && matchesSearch
  })
})

const nextImage = (product) => {
  if (product?.images?.length) {
    product.currentImgIndex = (product.currentImgIndex + 1) % product.images.length
  }
}

const prevImage = (product) => {
  if (product?.images?.length) {
    product.currentImgIndex = (product.currentImgIndex - 1 + product.images.length) % product.images.length
  }
}

const submitNewProduct = () => {
  const newProduct = {
    id: Date.now(),
    title: newProductData.value.title,
    price: Number(newProductData.value.price),
    category: newProductData.value.category,
    weight: newProductData.value.weight,
    desc: newProductData.value.desc,
    badge: newProductData.value.badge.trim() || null,
    currentImgIndex: 0,
    images: []
  }
  allProducts.value.unshift(newProduct)
  newProductData.value = initialFormState()
  isFormOpen.value = false
}

const handleDeleteProduct = (id) => {
  allProducts.value = allProducts.value.filter(product => product.id !== id)
}
</script>

<template>
  <div style="background-color: #FDFBF7; min-height: 100vh; font-family: sans-serif; color: #1a1a1a; padding: 40px 20px; box-sizing: border-box;">
    <div style="max-width: 900px; margin: 0 auto;">
  
      <header style="text-align: center; margin-bottom: 40px; border-bottom: 1px solid #1a1a1a; padding-bottom: 30px;">
        <div style="color: #888; font-size: 10px; font-weight: bold; letter-spacing: 3px; margin-bottom: 10px;">
          ISSUE NO. 01 / 2026
        </div>
        <div style="display: flex; flex-wrap: wrap; align-items: center; justify-content: center; gap: 30px;">
          <div style="flex: 1; min-width: 280px;">
            <h1 style="font-weight: normal; font-size: 36px; margin: 10px 0; text-align: center;">Авторская кондитерская</h1>
            <div style="width: 50px; height: 1px; background-color: #1a1a1a; margin: 15px auto;"></div>
            <p style="max-width: 500px; font-size: 13px; color: #444; margin: 0 auto; line-height: 1.6;">
              Я верю, что идеальный десерт — это не просто сахар и крем. Это точный расчет пропорций, геометрия слоев и честные локальные продукты. Каждое изделие создается вручную с бескомпромиссным вниманием к деталям.
            </p>
          </div>
          <div v-if="bannerImg" style="width: 200px; height: 200px; border-radius: 50%; overflow: hidden; border: 1px solid #1a1a1a;">
            <img :src="bannerImg" alt="Кондитерская" style="width: 100%; height: 100%; object-fit: cover; filter: grayscale(0.2) contrast(1.05);" />
          </div>
        </div>
      </header>

      <section style="background-color: white; padding: 20px; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.03); margin-bottom: 40px; border: 1px solid #eee; position: relative;">
        <h5 style="margin: 0 0 15px 0; font-size: 12px; text-transform: uppercase; color: #888; letter-spacing: 1px;">Панель управления</h5>
        <div style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 15px;">
          <div style="flex: 1; min-width: 200px;">
            <label style="font-size: 12px; color: #555; display: block; margin-bottom: 5px;">Размер шрифта цены (px):</label>
            <input type="number" v-model.number="fontSize" min="14" max="30" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; box-sizing: border-box;">
          </div>
          <div style="flex: 1; min-width: 200px;">
            <label style="font-size: 12px; color: #555; display: block; margin-bottom: 5px;">Поиск по названию:</label>
            <input type="text" v-model="searchQuery" placeholder="Введите название..." style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; box-sizing: border-box;">
          </div>
        </div>
        <div style="text-align: right;">
          <button @click="isFormOpen = true" style="background-color: #1a1a1a; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-size: 13px; cursor: pointer; font-weight: bold;">
            + Добавить новинку
          </button>
        </div>

        <div v-if="isFormOpen" style="position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: rgba(0,0,0,0.5); display: flex; align-items: center; justify-content: center; z-index: 999; padding: 20px; box-sizing: border-box;">
          <div style="background: #FDFBF7; padding: 30px; border-radius: 8px; max-width: 500px; width: 100%; box-shadow: 0 10px 25px rgba(0,0,0,0.2); border: 1px solid #1a1a1a; position: relative; text-align: left;">
            <h3 style="margin-top: 0; margin-bottom: 20px; font-weight: normal; font-size: 22px; text-align: center; border-bottom: 1px solid #1a1a1a; padding-bottom: 10px; color: #1a1a1a;">Новое изделие в меню</h3>
            <form @submit.prevent="submitNewProduct" style="display: flex; flex-direction: column; gap: 12px;">
              <div>
                <label style="font-size: 11px; text-transform: uppercase; color: #555; display: block; margin-bottom: 3px;">Название изделия *</label>
                <input type="text" v-model="newProductData.title" required placeholder="Например: Кекс лимонный" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; box-sizing: border-box;">
              </div>
              <div style="display: flex; gap: 15px;">
                <div style="flex: 1;">
                  <label style="font-size: 11px; text-transform: uppercase; color: #555; display: block; margin-bottom: 3px;">Цена (₽) *</label>
                  <input type="number" v-model.number="newProductData.price" required min="1" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; box-sizing: border-box;">
                </div>
                <div style="flex: 1;">
                  <label style="font-size: 11px; text-transform: uppercase; color: #555; display: block; margin-bottom: 3px;">Вес / Объем *</label>
                  <input type="text" v-model="newProductData.weight" required placeholder="Например: 150 г" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; box-sizing: border-box;">
                </div>
              </div>
              <div style="display: flex; gap: 15px;">
                <div style="flex: 1;">
                  <label style="font-size: 11px; text-transform: uppercase; color: #555; display: block; margin-bottom: 3px;">Категория</label>
                  <select v-model="newProductData.category" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; box-sizing: border-box; background: white;">
                    <option value="desserts">Наши десерты</option>
                    <option value="bakery">Хлеб и выпечка</option>
                  </select>
                </div>
                <div style="flex: 1;">
                  <label style="font-size: 11px; text-transform: uppercase; color: #555; display: block; margin-bottom: 3px;">Бейдж</label>
                  <input type="text" v-model="newProductData.badge" placeholder="Например: Хит, NEW" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; box-sizing: border-box;">
                </div>
              </div>
              <div>
                <label style="font-size: 11px; text-transform: uppercase; color: #555; display: block; margin-bottom: 3px;">Описание состава и вкуса *</label>
                <textarea v-model="newProductData.desc" required rows="3" placeholder="Опишите текстуру..." style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; box-sizing: border-box; resize: none; font-family: sans-serif;"></textarea>
              </div>
              <div style="display: flex; gap: 10px; margin-top: 15px;">
                <button type="button" @click="isFormOpen = false" style="flex: 1; padding: 10px; background: transparent; border: 1px solid #1a1a1a; color: #1a1a1a; border-radius: 4px; cursor: pointer; font-size: 13px;">Отмена</button>
                <button type="submit" style="flex: 1; padding: 10px; background: #1a1a1a; color: white; border: none; border-radius: 4px; cursor: pointer; font-size: 13px; font-weight: bold;">Сохранить в меню</button>
              </div>
            </form>
          </div>
        </div>
      </section>

      <nav style="display: flex; gap: 15px; margin-bottom: 30px;">
        <button :style="currentCategory === 'all' ? 'background: #1a1a1a; color: white;' : 'background: white; color: #1a1a1a;'"
                style="flex: 1; padding: 12px; border: 1px solid #1a1a1a; border-radius: 4px; font-size: 13px; text-transform: uppercase; cursor: pointer; font-weight: bold;"
                @click="currentCategory = 'all'">
          Все изделия
        </button>
        <button :style="currentCategory === 'bakery' ? 'background: #1a1a1a; color: white;' : 'background: white; color: #1a1a1a;'"
                style="flex: 1; padding: 12px; border: 1px solid #1a1a1a; border-radius: 4px; font-size: 13px; text-transform: uppercase; cursor: pointer; font-weight: bold;"
                @click="currentCategory = 'bakery'">
          Хлеб и выпечка
        </button>
        <button :style="currentCategory === 'desserts' ? 'background: #1a1a1a; color: white;' : 'background: white; color: #1a1a1a;'"
                style="flex: 1; padding: 12px; border: 1px solid #1a1a1a; border-radius: 4px; font-size: 13px; text-transform: uppercase; cursor: pointer; font-weight: bold;"
                @click="currentCategory = 'desserts'">
          Наши десерты
        </button>
      </nav>
                      
      <main class="row g-4">
        <div v-if="filteredProducts.length === 0" class="col-12 text-center" style="color: #888; padding: 40px 0;">
          Ничего не найдено в этой категории.
        </div>
        
        <ProductCard 
          v-else 
          v-for="product in filteredProducts" 
          :key="product.id"
          :product="product"
          :font-size="fontSize"
          @next-img="nextImage(product)"
          @prev-img="prevImage(product)"
          @delete-product="handleDeleteProduct"
        />
      </main>

    </div>
  </div>
</template>

<style scoped>
.col-12 > div {
  transition: transform 0.3s ease, box-shadow 0.3s ease !important;
}
.col-12 > div:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.08) !important;
}

button[style*="border: 1px solid #dc3545"] {
  transition: all 0.25s ease !important;
}
button[style*="border: 1px solid #dc3545"]:hover {
  background-color: #dc3545 !important;
  color: white !important;
}
button[style*="background: rgba(255,255,255,0.8)"] {
  transition: background 0.2s ease !important;
}
button[style*="background: rgba(255,255,255,0.8)"]:hover {
  background: rgba(255, 255, 255, 1) !important;
  transform: translateY(-50%) scale(1.1) !important;
}
</style>
