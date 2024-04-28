<template>
    <div class="shoe-card">
      <div class="shoe-details">
        <div class="shoe-image" :style="{ backgroundColor: selectedColor }"></div>
        <h2>{{ shoe.brand }}</h2>
        <p>{{ shoe.model }}</p>
        <p>Price: ${{ shoe.price }}</p>
        <div class="size-selector">
          <div
            v-for="size in sizes"
            :key="size"
            class="size"
            @click="selectSize(size)"
            :class="{ 'selected': size === selectedSize }"
          >{{ size }}</div>
        </div>
        <div class="color-selector"> 
        <div
          v-for="(color, index) in colors" 
          :key="index"
          class="color"
          :style="{ backgroundColor: color }"
          @click="selectColor(color)"
          :class="{ 'selected': color === selectedColor }"
        ></div>
        <div 
          class="color" 
          style="background-color: #ADD8E6;"
          @click="selectColor('#ADD8E6')"  
          :class="{ 'selected': selectedColor === '#ADD8E6' }" 
        ></div> 
      </div> 

    </div>
        <button @click="buyNow">Buy</button>
    </div>
  
  </template>
  

<script>
export default {
  props: {
    shoe: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      selectedColor: this.shoe.colors && this.shoe.colors.length > 0 ? this.shoe.colors[0] : '#FFFFFF',
      selectedSize: null,
      colors: this.shoe.colors || [],
      sizes: ['S', 'M', 'L', 'XL']
    };
  },
  methods: {
    selectColor(color) {
      this.selectedColor = color;
    },
    selectSize(size) {
      this.selectedSize = size;
    },
    buyNow() {
      if (this.selectedSize) {
        alert(`You have selected color: ${this.selectedColor}, size: ${this.selectedSize}. Thank you for your purchase!`);
      } else {
        alert('Please select a size before buying.');
      }
    }
  }
};
</script>

<style>
.shoe-card {
  display: flex;
  max-width: 500px;
  margin: 20px auto;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  background-color: #5a5a5a;
  flex-direction: column; 

}

.color-selector {
    margin-top: 10px;
  display: flex;
  justify-content: center;
  margin-bottom: 10px;

}

.color {
  width: 30px;
  height: 30px;
  border-radius: 5px;
  margin: 0 5px;
  cursor: pointer;
}

.color.selected {
  border: 2px solid #333;
}

.color-picker {
  height: 30px;
  margin-bottom: 10px;
}

.shoe-details {
  flex: 1;
  padding: 10px;
  display: flex;
  flex-direction: column;
}

.shoe-image {
  height: 200px;
  margin-bottom: 10px;
  border-radius: 10px;
}

.size-selector {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.size {
  padding: 5px 10px;
  margin: 0 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
  cursor: pointer;
}

.size.selected {
  background-color: #FF6347;
  color: white;
}

button {
  padding: 10px;
  width: 100%;
  background-color: #FF6347;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 10px;
}

button:hover {
  background-color: #FF4500;
}
</style>