<template>
  <!-- Сетка Bootstrap (col-12 на мобильных, col-md-6 на планшете/ПК) -->
  <div class="col-12 col-md-6 mb-4 d-flex">
    
    <!--  карточка -->
    <div style="background-color: white; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.05); padding: 20px; display: flex; flex-direction: column; height: 100%; box-sizing: border-box; width: 100%;">
         
      <!--  картинка или заглушка слайдера -->
      <div style="height: 220px; width: 100%; position: relative; background-color: #f5f4f0; border-radius: 6px; overflow: hidden; margin-bottom: 15px; display: flex; align-items: center; justify-content: center;">
        <div v-if="product.badge" style="position: absolute; top: 10px; left: 10px; background: rgba(255,255,255,0.9); color: #1a1a1a; padding: 3px 8px; border: 1px solid #1a1a1a; font-size: 9px; text-transform: uppercase; font-weight: bold; z-index: 2;">
          {{ product.badge }}
        </div>
        
        <!-- Кнопка Слайдера Левая -->
        <button v-if="product.images && product.images.length > 1" @click="$emit('prev-img')" style="position: absolute; left: 8px; top: 50%; transform: translateY(-50%); background: rgba(255,255,255,0.8); border: none; width: 26px; height: 26px; border-radius: 50%; cursor: pointer; z-index: 3; font-weight: bold; font-size: 14px;">‹</button>
        
        <!-- Вывод картинки, иначе заглушка  -->
        <img v-if="product.images && product.images.length > 0" :src="product.images[product.currentImgIndex]" :alt="product.title" style="width: 100%; height: 100%; object-fit: cover;" />
        <div v-else style="color: #777; font-size: 13px; text-transform: uppercase; letter-spacing: 1px;">[ Кондитерское изделие ]</div>
        
        <!-- Кнопка Слайдера Правая -->
        <button v-if="product.images && product.images.length > 1" @click="$emit('next-img')" style="position: absolute; right: 8px; top: 50%; transform: translateY(-50%); background: rgba(255,255,255,0.8); border: none; width: 26px; height: 26px; border-radius: 50%; cursor: pointer; z-index: 3; font-weight: bold; font-size: 14px;">›</button>
      
        <!-- Точки слайдера -->
        <div v-if="product.images && product.images.length > 1" style="position: absolute; bottom: 10px; display: flex; gap: 5px; z-index: 3;">
          <span v-for="(img, idx) in product.images" :key="idx" 
                :style="idx === product.currentImgIndex ? 'background: #1a1a1a; transform: scale(1.2);' : 'background: rgba(255,255,255,0.6);'"
                style="width: 6px; height: 6px; border-radius: 50%; transition: 0.2s;"></span>
        </div>
      </div>
      
      <!--  блок с выводом свойств через {{ }} -->
      <div style="text-align: center; display: flex; flex-direction: column; flex-grow: 1;">
        <h3 style="margin: 0 0 5px 0; font-size: 18px; font-weight: bold; color: #1a1a1a;">
          {{ product.title }}
        </h3>
        
        <div style="font-size: 12px; color: #888; margin-bottom: 10px;">
          {{ product.weight }}
        </div>
        
        <p style="font-size: 13px; color: #555; line-height: 1.5; margin: 0 0 15px 0; flex-grow: 1;">
          {{ product.desc }}
        </p>
        
        <div style="margin-top: auto;">
          <div style="font-weight: bold; margin-bottom: 12px; color: #1a1a1a;" :style="{ 'font-size': fontSize + 'px' }">
            от {{ product.price }} ₽
          </div>
          <!--  Кнопка с кастомным событием $emit для удаления -->
          <button style="width: 100%; padding: 8px; background: transparent; border: 1px solid #dc3545; color: #dc3545; border-radius: 4px; font-size: 12px; cursor: pointer; transition: 0.2s;"
                  @click="$emit('delete-product', product.id)">
            Удалить из меню
          </button>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  // props
  props: {
    product: { type: Object, required: true },
    fontSize: { type: Number, required: true }
  }
}
</script>
