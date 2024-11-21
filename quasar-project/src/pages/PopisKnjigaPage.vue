<template>
  <q-page padding>
    <!-- Tablica s podacima o knjigama -->
    <q-table
      :rows="books"     
      :columns="columns" 
      row-key="id"      
      bordered
      flat
      :rows-per-page-options="[5, 10, 15]"
      :pagination="pagination"
    >
      <template v-slot:top>
        <q-toolbar>
          <q-toolbar-title>
            Popis knjiga
          </q-toolbar-title>
        </q-toolbar>
      </template>
    </q-table>
  </q-page>
</template>

<script>
export default {
  name: 'BooksPage',
  data() {
    return {
      // Dummy podaci o knjigama
      books: [
        { id: 1, naslov: 'Na Drini cuprija', autor: 'Ivo Andric', opis: 'Roman o povijesti i sudbini mosta na Drini, kroz narativnu povijest i sudbine ljudi.', stanje: 25 },
        { id: 2, naslov: 'Ponos i predrasude', autor: 'Jane Austen', opis: 'Klasicni roman koji istrazuje teme ljubavi, obitelji i drustvenih normi.',stanje: 30 },
        { id: 3, naslov: 'Sto godina samoce', autor: 'Gabriel Garcia Marquez', opis: 'Jedan od najpoznatijih romana magicnog realizma, koji prikazuje povijest obitelji Buendía.', stanje: 15 },
        { id: 4, naslov: '1984', autor: 'George Orwell', opis: 'Distopijski roman koji se bavi temama totalitarizma i kontrole drustva.', stanje: 40 },
        { id: 5, naslov: 'Mali princ', autor: 'Antoine de Saint-Exupery', opis: 'Filozofski roman koji se bavi pitanjima zivota, ljubavi i prirode ljudskog postojanja.', stanje: 50 }
      ],

      // Definicija kolona u tablici
      columns: [
        { name: 'naslov', label: 'Naslov', align: 'left', field: row => row.naslov },
        { name: 'autor', label: 'Autor', align: 'left', field: row => row.autor },
        { name: 'opis', label: 'Opis', align: 'left', field: row => row.opis },
        { name: 'stanje', label: 'Stanje', align: 'center', field: row => row.stanje }
      ],

      // Pagination
      pagination: {
        page: 1,
        rowsPerPage: 5
      }
    };
  }
}
</script>

<style scoped>
/* Stilovi za tablicu, slike i ostalo */
.q-table {
  width: 100%;
  max-width: 100%;
}

img {
  border-radius: 4px;
}
</style>
