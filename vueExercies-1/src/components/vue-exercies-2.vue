<script setup lang="ts">
import { ref } from 'vue';

const imageText = ref('')
const howManyFavorite = ref(0)
const imageArr = ref([
    {
        id: 1,
        imageUrl: 'https://images.unsplash.com/photo-1749741335932-f5295ee9afd0?w=900&auto=format&fit=crop&q=60&ixlib=rb-4.1.0&ixid=M3wxMjA3fDF8MHxmZWF0dXJlZC1waG90b3MtZmVlZHwxfHx8ZW58MHx8fHx8',
        isFavorite: false
    }
])

const addImage = () => {
    // console.log("addImage Çalışıyor");

    let photo = {
        id: imageArr.value.length + 1,
        imageUrl: imageText.value,
        isFavorite: false
    }
    // console.log("photo bilgileri: ", photo);
    if (photo.imageUrl === "" ) {
        return
    }
    else {
        imageArr.value.push(photo)
    }


    // console.log('imageArr durumu', imageArr.value)
}

const addFavorite = (id) => {
    let fav = imageArr.value.find(img => img.id === id);
    howManyFavorite.value++
    return fav.isFavorite = true
}

const removePhotos = (index) => {
    imageArr.value.splice(index,1)
    howManyFavorite.value--
}


</script>


<template>

    <form @submit.prevent="addImage">
        <input type="text" placeholder="paste your photo link" v-model="imageText">
        <button type="submit">Add Image</button>
    </form>
    <div>
        <span>How many Fav: {{ howManyFavorite }}</span>
        <div>
            <div class="img-div" v-for="item in imageArr" :key="item.id">
                <img :src="item.imageUrl" :alt="item.id">
                <span v-if="item.isFavorite === true">Favoride</span>
                <span v-else></span>
                <button @click="addFavorite(item.id)">Favoriye ekle</button>
                <button @click="removePhotos(index)">Sil</button>
            </div>
        </div>

    </div>
</template>


<style scoped>
.img-div {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

img {
    width: 300px;
    height: 300px;
    padding: 10px;
}
</style>