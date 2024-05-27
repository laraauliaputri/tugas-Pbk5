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
        <q-input outlined dense v-model="searchQuery" class="q-mb-xs" placeholder="Cari K-Pop Favoritmu...">
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
        class="bg-dark q-mt-lg q-mb-lg"
      >
        <q-carousel-slide
          v-for="(featured, index) in featuredItems"
          :key="index"
          :name="featured.name"
          :img-src="featured.image"
        >
          <div class="absolute-bottom text-white text-center q-pa-sm" style="background: rgba(0, 0, 0, 0.5)">
          </div>
        </q-carousel-slide>
      </q-carousel>
      <!-- End Carousel Section -->

      <div class="row q-col-gutter-md q-pt-md">
        <q-card
          v-for="(album, index) in albums"
          :key="index"
          class="col-xs-12 col-sm-6 col-md-4 col-lg-3 q-hover-shadow q-mb-md"
        >
          <q-img :src="album.image" class="q-mb-sm image-hover" />
          <q-card-section>
            <div class="text-subtitle1 text-black">{{ album.name }}</div>
            <div class="text-caption text-black">{{ album.description }}</div>
            <div class="text-h6 text-primary">{{ album.price }}</div>
            <q-rating :value="album.rating" max="5" size="16px" readonly />
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
    const albums = [
      {
        name: "lightstick BTS",
        description: "Lightstick BTS ARMY Bomb adalah aksesori esensial bagi penggemar BTS (ARMY). Dengan desain elegan dan kemampuan sinkronisasi warna melalui Bluetooth, lightstick ini membuat pengalaman konser lebih hidup dan berkesan",
        image: "https://i.pinimg.com/originals/bc/05/a6/bc05a6b3ca5bf62b8cf2df418b28c240.jpg",
        price: "$50",
        rating: 5
      },
      {
        name: "Album TXT - The Dream Chapter: BLUE HOUR",
        description: "The Dream Chapter: BLUE HOUR! Terdiri dari 128 halaman photobook yang memukau, CD dengan lagu-lagu pilihan, dua stiker kertas unik, serta kertas lirik untuk bernyanyi bersama, ",
        image: "https://i.pinimg.com/originals/14/97/ca/1497ca1394315e6bfc3672bf45d44a23.jpg",
        price: "$30",
        rating: 5
      },
      { 
         name: "keychan mingyu",
        description: "Terbuat dari bahan berkualitas tinggi, keychain ini tahan lama dan cocok untuk digunakan sehari-hari. Tambahkan sentuhan gaya pribadi pada kunci, tas, atau barang-barang lainnya Anda dengan keychain Mingyu yang menggemaskan ini.  ",
        image: "https://i.pinimg.com/originals/bf/b1/2d/bfb12d16550c48a91f5fbea3ddf13ec1.jpg",
        price: "$3",
        rating: 5
      },
      { 
         name: "Black Pink Born Pink World Tour Hoodie",
        description: "Dapatkan penampilan street-style yang keren dengan hoodie resmi dari tur konser Black Pink Born Pink World Tour! Hoodie ini dirancang dengan logo tur yang mencolok dan desain yang modern, memberikan nuansa edgy yang sesuai dengan gaya musik mereka. Dibuat dari bahan berkualitas tinggi yang nyaman dipakai sepanjang hari",
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
        description: "Nikmati koleksi merchandise resmi dari ITZY dengan tema Born to be! Koleksi ini menghadirkan berbagai printilan menarik yang dirancang khusus untuk para MIDZY ",
        image: "https://i.pinimg.com/originals/0f/94/b9/0f94b9e0caa11c2e9cba4ba7f4819c0c.jpg",
        price: "$50",
        rating: 5
      },
      { 
         name: "BT21 Minini Monitor Figure",
        description: "BT21 Minini Monitor Figure! Figur mini yang lucu ini dirancang untuk dipasang di atas monitor, Setiap figur menggambarkan karakter BT21 favorit Anda dalam pose menggemaskan, terbuat dari bahan berkualitas tinggi yang tahan lama dan detail yang menawan",
        image: "https://i.pinimg.com/originals/76/08/84/7608848b5971fbfc1514a688569bdb7b.jpg",
        price: "$15",
        rating: 4
      },
      { 
         name: "Map Of the Soul 7 ",
        description: " adalah album studio ketujuh dari BTS, dirilis pada 21 Februari 2020 oleh Big Hit Entertainment. Album ini mengeksplorasi tema identitas dan introspeksi, mencakup 20 lagu yang menggabungkan berbagai genre seperti pop, hip-hop, dan R&B. Beberapa lagu populer dalam album ini adalah Boy with Luv (feat. Halsey), Black Swan, ON, dan Louder than Bombs.",
        image: "https://i.pinimg.com/originals/50/dd/fc/50ddfcd184d8ba0af9076a79ec2d91bc.jpg",
        price: "$40 ",
        rating: 5
      },
    ]

    const featuredItems = [
      {
        name: "lightstick BTS",
        description: "Lightstick BTS ARMY Bomb adalah aksesori esensial bagi penggemar BTS (ARMY). Dengan desain elegan dan kemampuan sinkronisasi warna melalui Bluetooth, lightstick ini membuat pengalaman konser lebih hidup dan berkesan",
        image: "https://i.pinimg.com/originals/b2/9f/59/b29f59501bf34fd645dc2e44dae69b60.jpg",
      },
      {
        name: "Album TXT - The Dream Chapter: BLUE HOUR",
        description: "The Dream Chapter: BLUE HOUR! Terdiri dari 128 halaman photobook yang memukau, CD dengan lagu-lagu pilihan, dua stiker kertas unik, serta kertas lirik untuk bernyanyi bersama, ",
        image: "https://i.pinimg.com/originals/ee/65/6e/ee656e2d1c75ef93b0161a5f0187a204.jpg",
      },
      {
        name: "Black Pink Born Pink World Tour Hoodie",
        description: "Dapatkan penampilan street-style yang keren dengan hoodie resmi dari tur konser Black Pink Born Pink World Tour! Hoodie ini dirancang dengan logo tur yang mencolok dan desain yang modern, memberikan nuansa edgy yang sesuai dengan gaya musik mereka. Dibuat dari bahan berkualitas tinggi yang nyaman dipakai sepanjang hari",
        image: "https://i.pinimg.com/originals/13/2b/32/132b327863bb64d146e52ad3bfc8ac49.jpg",
      },
      {
        name: "Map Of the Soul 7 ",
        description: " adalah album studio ketujuh dari BTS, dirilis pada 21 Februari 2020 oleh Big Hit Entertainment. Album ini mengeksplorasi tema identitas dan introspeksi, mencakup 20 lagu yang menggabungkan berbagai genre seperti pop, hip-hop, dan R&B. Beberapa lagu populer dalam album ini adalah Boy with Luv (feat. Halsey), Black Swan, ON, dan Louder than Bombs.",
        image: "https://i.pinimg.com/originals/05/ed/38/05ed380a74d24e8c5c52a11a165e58f0.jpg",
      },
    ]

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },
      searchQuery,
      albums,
      featuredItems,
      slide
    }
  }
}
</script>

<style scoped>
/* Gaya khusus untuk header dan tab */
.bg-gradient-to-r {
  background: linear-gradient(to right, #f72585, #b5179e, #7209b7, #560bad, #480ca8, #3a0ca3, #3f37c9, #4361ee, #4895ef, #4cc9f0);
}

/* Gaya khusus untuk ikon pencarian */
.q-input__suffix .q-icon {
  font-size: 20px;
}

/* Gaya khusus untuk card */
.q-card {
  background-color: #ffffff;
}

/* Margin bawah untuk gambar */
.image-hover {
  margin-bottom: 10px;
}

/* Gaya teks untuk nama album */
.text-subtitle1 {
  font-size: 1.2rem;
  color: #333333;
  font-weight: bold;
}

/* Gaya teks untuk deskripsi album */
.text-caption {
  font-size: 1rem;
  color: #666666;
}

/* Gaya teks untuk harga album */
.text-h6 {
  font-size: 1.2rem;
  color: #007bff; /* Warna biru */
  font-weight: bold;
}

/* Gaya bintang rating */
.q-rating {
  color: #ffc107; /* Warna kuning */
}

/* Gaya untuk carousel */
.q-carousel {
  position: relative; /* Mengatur posisi carousel */
  overflow: hidden; /* Menghilangkan overflow yang tidak diinginkan */
  border-radius: 10px; /* Membuat sudut carousel sedikit melengkung */
}

/* Gaya untuk slide dalam carousel */
.q-carousel-slide {
  position: relative; /* Mengatur posisi slide */
  height: 100%; /* Menjadikan slide setinggi carousel */
}

/* Gaya untuk teks deskripsi pada slide */
.slide-description {
  position: absolute; /* Mengatur posisi absolut */
  bottom: 20px; /* Jarak dari bawah */
  left: 20px; /* Jarak dari kiri */
  right: 20px; /* Jarak dari kanan */
  color: #ffffff; /* Warna teks putih */
  text-align: center; /* Posisi teks di tengah */
  background-color: rgba(0, 0, 0, 0.5); /* Warna latar belakang semi-transparent */
  border-radius: 5px; /* Membuat sudut teks sedikit melengkung */
  padding: 10px; /* Padding untuk konten teks */
  opacity: 0; /* Awalnya tidak terlihat */
  transition: opacity 0.3s ease; /* Efek transisi untuk muncul */
}

/* Efek hover untuk slide */
.q-carousel-slide:hover .slide-description {
  opacity: 1; /* Munculkan deskripsi saat dihover */
}

/* Gaya untuk navigasi carousel */
.q-carousel-navigation, .q-carousel-control {
  color: #ffffff; /* Warna ikon navigasi */
}

/* Gaya untuk titik navigasi */
.q-carousel-pagination {
  position: absolute; /* Mengatur posisi absolut */
  bottom: 10px; /* Jarak dari bawah */
  left: 50%; /* Posisi horizontal di tengah */
  transform: translateX(-50%); /* Pusatkan horizontal */
}

/* Gaya untuk titik navigasi aktif */
.q-carousel-pagination button.active {
  background-color: #ffffff; /* Warna latar belakang putih */
  box-shadow: 0 0 3px rgba(0, 0, 0, 0.3); /* Efek bayangan saat aktif */
}

/* Gaya untuk panah navigasi */
.q-carousel-navigation button {
  background-color: rgba(0, 0, 0, 0.5); /* Warna latar belakang semi-transparent */
  border-radius: 50%; /* Membuat sudut tombol bundar */
}

/* Efek hover untuk panah navigasi */
.q-carousel-navigation button:hover {
  background-color: rgba(0, 0, 0, 0.8); /* Warna latar belakang saat dihover */
}

/* Gaya untuk panah kiri */
.q-carousel-navigation .q-carousel-prev {
  left: 20px; /* Jarak dari kiri */
}

/* Gaya untuk panah kanan */
.q-carousel-navigation .q-carousel-next {
  right: 20px; /* Jarak dari kanan */
}

/* Gaya untuk carousel */
.bg-dark {
  background: #333;
}

/* Margin bawah untuk carousel */
.q-mb-md {
  margin-bottom: 16px;
}

/* Margin atas untuk carousel */
.q-mt-lg {
  margin-top: 32px;
}

/* Margin bawah untuk carousel */
.q-mb-lg {
  margin-bottom: 32px;
}

/* Margin bawah untuk navigasi */
.q-mb-md {
  margin-bottom: 16px;
}

</style>
