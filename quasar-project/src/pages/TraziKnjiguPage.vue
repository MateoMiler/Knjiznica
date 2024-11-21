<template>
  <q-page padding>
    <!-- Pretraživanje -->
    <div class="q-pa-md">
      <q-input 
        v-model="searchQuery" 
        label="Unesite pojam za pretragu" 
        debounce="300"
        outlined
        @input="performSearch"
      />
      
      <q-checkbox 
        v-model="searchByAuthor" 
        label="Pretraži po autoru" 
        left-label
        @change="performSearch"
      />
      
      <q-checkbox 
        v-model="searchByTitle" 
        label="Pretraži po naslovu" 
        left-label
        @change="performSearch"
      />
      
      <q-btn 
        label="Traži" 
        color="primary" 
        @click="performSearch" 
      />
    </div>

    <!-- Tablica sa rezultatima -->
    <q-table 
      :rows="filteredBooks" 
      :columns="columns" 
      row-key="id"
    >
      <template v-slot:top>
        <q-banner class="bg-primary text-white" dense>
          <div class="text-h6">Rezultati pretrage</div>
        </q-banner>
      </template>
    </q-table>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '', // Pojam za pretragu
      searchByAuthor: false, // Filter za pretragu po autoru
      searchByTitle: false, // Filter za pretragu po naslovu
      books: [
        { id: 1, naslov: 'Na Drini cuprija', autor: 'Ivo Andric' },
        { id: 2, naslov: 'Ponos i predrasude', autor: 'Jane Austen' },
        { id: 3, naslov: 'Sto godina samoce', autor: 'Gabriel Garcia Marquez' },
        { id: 4, naslov: '1984', autor: 'George Orwell' },
        { id: 5, naslov: 'Mali princ', autor: 'Antoine de Saint-Exupery' }
        // Dodajte više knjiga po potrebi
      ],
      columns: [
        { name: 'naslov', label: 'Naslov', align: 'left', field: 'naslov' },
        { name: 'autor', label: 'Autor', align: 'left', field: 'autor' }
      ],
    };
  },
  computed: {
    filteredBooks() {
      const query = this.searchQuery.toLowerCase();
      
      // Filtriramo knjige prema odabranim kriterijumima
      return this.books.filter(book => {
        const matchTitle = book.naslov.toLowerCase().includes(query);
        const matchAuthor = book.autor.toLowerCase().includes(query);

        if (this.searchByAuthor && this.searchByTitle) {
          // Pretražuje se i po naslovu i po autoru
          return matchTitle || matchAuthor;
        } else if (this.searchByAuthor) {
          // Pretražuje se samo po autoru
          return matchAuthor;
        } else if (this.searchByTitle) {
          // Pretražuje se samo po naslovu
          return matchTitle;
        } else {
          // Ako ništa nije označeno, pokazujemo samo knjige koje sadrže pojam u naslovu ili autoru
          return matchTitle || matchAuthor;
        }
      });
    },
  },
  methods: {
    performSearch() {
      // Ovdje možete implementirati dodatnu logiku pretrage, ako je potrebno
      console.log('Traženje prema:', this.searchQuery);
      console.log('Pretražuje se po autoru:', this.searchByAuthor);
      console.log('Pretražuje se po naslovu:', this.searchByTitle);
    },
  },
};
</script>

<style scoped>
.q-table {
  margin-top: 20px;
}
</style>
