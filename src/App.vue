<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="bg-gradient-to-r from-pink-500 to-purple-600 text-white q-mb-md">
      <q-toolbar class="q-pa-none q-gutter-md" justify="between">
        <q-btn dense flat round icon="menu" color="white" @click="toggleLeftDrawer" />
        <q-toolbar-title class="text-h6">
          Galaxy Groove K-Pop Store
        </q-toolbar-title>
        <q-tabs align="left" class="text-white">
          <q-tab to="/home" label="Beranda" />
          <q-tab to="/promo" label="Promo" />
          <q-tab to="/terbaru" label="Terbaru" />
          <q-tab to="/aksesoris" label="Aksesoris" />
          <q-tab to="/album-musik" label="Album Musik" />
          <q-tab to="/merchandise" label="Merchandise" />
          <q-tab to="/kosmetik-skincare" label="Kosmetik dan Skincare" />
        </q-tabs>
        <q-input outlined dense v-model="searchQuery" class="q-mb-xs search-input" placeholder="Cari K-Pop Favoritmu...">
          <template v-slot:append>
            <q-icon name="search" class="cursor-pointer text-white" />
          </template>
        </q-input>
      </q-toolbar>
    </q-header>

    <q-page-container class="q-pa-md">
      <!-- Carousel Section -->
      <q-carousel
        v-model="slide"
        animated
        infinite
        swipeable
        navigation
        control-color="white"
        height="400px"
        autoplay
        autoplay-interval="3000"
        class="bg-dark q-mt-lg q-mb-lg carousel-container"
      >
        <q-carousel-slide
          v-for="(featured, index) in featuredItems"
          :key="index"
          :name="featured.name"
          :img-src="featured.image"
          class="carousel-slide"
        >
          <div class="absolute-bottom text-white text-center q-pa-sm slide-caption">
            {{ featured.name }}
          </div>
        </q-carousel-slide>
      </q-carousel>
      <!-- End Carousel Section -->

      <div class="row q-col-gutter-md q-pt-md">
        <q-card
          v-for="(album, index) in albums"
          :key="index"
          class="col-xs-12 col-sm-6 col-md-4 col-lg-3 q-hover-shadow q-mb-md album-card"
        >
          <q-img :src="album.image" class="q-mb-sm image-hover card-image" />
          <q-card-section class="card-section">
            <div class="text-subtitle2">{{ album.name }}</div>
            <div class="text-caption">{{ album.description }}</div>
            <div class="text-h6 text-primary">{{ album.price }}</div>
            <q-rating :value="album.rating" max="5" size="16px" readonly />
            <q-btn dense flat icon="delete" color="red" @click="deleteAlbum(index)">Hapus</q-btn>
          </q-card-section>
        </q-card>
      </div>
    </q-page-container>

    <q-footer elevated class="bg-gradient-to-r from-pink-500 to-purple-600 text-white">
      <q-toolbar class="q-pa-none q-gutter-md" justify="center">
        <q-toolbar-title style="font-size: 12px; text-align: center;">
          © 2024 Stellar Vibes. All rights reserved.
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>

    <q-drawer show-if-above v-model="leftDrawerOpen" side="left" bordered>
      <q-list>
        <q-item clickable v-ripple to="/home">
          <q-item-section>
            <q-item-label class="text-lg font-semibold">Beranda</q-item-label>
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple to="/top-seller">
          <q-item-section>
            <q-item-label class="text-lg font-semibold">Top Seller</q-item-label>
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple to="/tentang-kami">
          <q-item-section>
            <q-item-label class="text-lg font-semibold">Tentang Kami</q-item-label>
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple to="/kontak">
          <q-item-section>
            <q-item-label class="text-lg font-semibold">Kontak</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>
  </q-layout>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const leftDrawerOpen = ref(false)
    const searchQuery = ref('')
    const slide = ref(0)
    const albums = ref([
      {
        name: "Lightstick BTS",
        description: "Lightstick BTS ARMY Bomb adalah aksesori esensial bagi penggemar BTS (ARMY). Dengan desain elegan dan kemampuan sinkronisasi warna melalui Bluetooth, lightstick ini membuat pengalaman konser lebih hidup dan berkesan.",
        image: "https://i.pinimg.com/originals/bc/05/a6/bc05a6b3ca5bf62b8cf2df418b28c240.jpg",
        price: "$50",
        rating: 5
      },
      {
        name: "Album TXT - The Dream Chapter: BLUE HOUR",
        description: "The Dream Chapter: BLUE HOUR! Terdiri dari 128 halaman photobook yang memukau, CD dengan lagu-lagu pilihan, dua stiker kertas unik, serta kertas lirik untuk bernyanyi bersama.",
        image: "https://i.pinimg.com/originals/14/97/ca/1497ca1394315e6bfc3672bf45d44a23.jpg",
        price: "$30",
        rating: 5
      },
      { 
        name: "Keychain Mingyu",
        description: "Terbuat dari bahan berkualitas tinggi, keychain ini tahan lama dan cocok untuk digunakan sehari-hari. Tambahkan sentuhan gaya pribadi pada kunci, tas, atau barang-barang lainnya Anda dengan keychain Mingyu yang menggemaskan ini.",
        image: "https://i.pinimg.com/originals/bf/b1/2d/bfb12d16550c48a91f5fbea3ddf13ec1.jpg",
        price: "$3",
        rating: 5
      },
      { 
        name: "Black Pink Born Pink World Tour Hoodie",
        description: "Dapatkan penampilan street-style yang keren dengan hoodie resmi dari tur konser Black Pink Born Pink World Tour! Hoodie ini dirancang dengan logo tur yang mencolok dan desain yang modern, memberikan nuansa edgy yang sesuai dengan gaya musik mereka. Dibuat dari bahan berkualitas tinggi yang nyaman dipakai sepanjang hari.",
        image: "https://i.pinimg.com/originals/b5/53/99/b5539954f7d32cd9e16df1ca7217b30a.jpg",
        price: "$27.99",
        rating: 5
      },
      { 
        name: "Photocard MARK LEE",
        description: "Dibuat dengan kualitas tinggi, photocard ini cocok untuk dikoleksi atau dipajang sebagai bagian dari memorabilia NCT Anda. Tambahkan ke koleksi Anda dan tunjukkan dukungan Anda kepada Mark Lee dan NCT!",
        image: "https://i.pinimg.com/originals/51/40/cf/5140cf78d5511b03c9f28bb6154243a9.jpg",
        price: "$20",
        rating: 5
      },
      { 
        name: "ITZY Born to be Merchandise Collection",
        description: "Nikmati koleksi merchandise resmi dari ITZY dengan tema Born to be! Koleksi ini menghadirkan berbagai printilan menarik yang dirancang khusus untuk para MIDZY.",
        image: "https://i.pinimg.com/originals/0f/94/b9/0f94b9e0caa11c2e9cba4ba7f4819c0c.jpg",
        price: "$50",
        rating: 5
      },
      { 
        name: "BT21 Minini Monitor Figure",
        description: "BT21 Minini Monitor Figure! Figur mini yang lucu ini dirancang untuk dipasang di atas monitor, Setiap figur menggambarkan karakter BT21 favorit Anda dalam pose menggemaskan, terbuat dari bahan berkualitas tinggi yang tahan lama dan detail yang menawan.",
        image: "https://i.pinimg.com/originals/76/08/84/7608848b5971fbfc1514a688569bdb7b.jpg",
        price: "$15",
        rating: 4
      },
      { 
        name: "Map Of the Soul 7",
        description: "Adalah album studio ketujuh dari BTS, dirilis pada 21 Februari 2020 oleh Big Hit Entertainment. Album ini mengeksplorasi tema-tema seperti pencarian jati diri dan perjalanan pribadi para anggota BTS.",
        image: "https://i.pinimg.com/originals/50/dd/fc/50ddfcd184d8ba0af9076a79ec2d91bc.jpg",
        price: "$25",
        rating: 5
      }
    ])

    const featuredItems = ref([
      {
        name: "BTS Poster",
        image: "https://i.pinimg.com/originals/b2/9f/59/b29f59501bf34fd645dc2e44dae69b60.jpg",
      },
      {
        name: "Enhypen",
        image: "https://i.pinimg.com/originals/05/ed/38/05ed380a74d24e8c5c52a11a165e58f0.jpg",
      },
      {
        name: "ALbum BTS",
        image: "https://i.pinimg.com/originals/13/2b/32/132b327863bb64d146e52ad3bfc8ac49.jpg",
      },
    ])

    const toggleLeftDrawer = () => {
      leftDrawerOpen.value = !leftDrawerOpen.value
    }

    const deleteAlbum = (index) => {
      albums.value.splice(index, 1);
    }

    return {
      leftDrawerOpen,
      searchQuery,
      slide,
      albums,
      featuredItems,
      toggleLeftDrawer,
      deleteAlbum
    }
  }
}
</script>

<style>
.image-hover {
  transition: transform 0.3s, opacity 0.3s;
  border-radius: 8px;
}

.image-hover:hover {
  transform: scale(1.05);
  opacity: 0.9;
}

.carousel-container {
  border-radius: 8px;
  overflow: hidden;
  position: relative;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.carousel-slide img {
  border-radius: 8px;
  transition: opacity 0.5s ease-in-out, transform 0.3s;
}

.carousel-slide img:hover {
  opacity: 0.8;
  transform: scale(1.05);
}

.slide-caption {
  background: rgba(0, 0, 0, 0.6);
  padding: 10px;
  border-radius: 8px;
  transition: background 0.3s ease-in-out;
}

.carousel-container:hover .slide-caption {
  background: rgba(0, 0, 0, 0.8);
}

.album-card {
  border-radius: 8px;
  transition: transform 0.2s, box-shadow 0.2s;
  height: 100px; /* Adjust the height here */
  margin: 48px;
}

.album-card:hover {
  transform: scale(1.05);
  box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.2);
}

.card-section {
  text-align: center;
  padding: 8px; /* Adjust the padding if necessary */
}

.card-image {
  height: 200px; /* Adjust the image height */
  object-fit: cover; /* Ensure the image covers the area */
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.search-input .q-field__native {
  color: white;
}

.search-input .q-field__append {
  background: rgba(255, 255, 255, 0.2);
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
}

.search-input input::placeholder {
  color: rgba(255, 255, 255, 0.5);
}

/* Gaya khusus untuk header dan tab */
.bg-gradient-to-r {
  background: linear-gradient(to right, #f72585, #b5179e, #7209b7, #560bad, #480ca8, #3a0ca3, #3f37c9, #4361ee, #4895ef, #4cc9f0);
}

.carousel-container:hover {
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
}

.q-btn {
  transition: background-color 0.3s, transform 0.3s;
}

.q-btn:hover {
  background-color: #ff4081;
  transform: translateY(-2px);
}

</style>
