<template>
  <div class="home">
    <!--<img alt="Vue logo" src="../assets/logo.png" />-->
    <!--<HelloWorld msg="Welcome to Your Vue.js App" />-->
    <ul>
      <li>limit: {{ limit }}</li>
      <li>page: {{ page }}</li>
      <li>totalData: {{ totalPage }}</li>
      <li>totalPage: {{ totalPage / limit }}</li>
      <li>counLimit: {{ counLimit }}</li>
    </ul>
    <table v-if="dataMasterLoop.length">
      <thead>
        <tr>
          <td>Id</td>
          <td>Nama</td>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(item, index) in dataMasterLoop"
          :key="`dataMasterKe${index}`"
        >
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
        </tr>
      </tbody>
    </table>
    <h1 v-else>Data Kosong</h1>
    <button :disabled="page == 1" @click="getData('prev')">Prev</button>
    <button
      v-for="ind in totalPage / limit"
      :key="`ind${ind}`"
      :disabled="ind == page"
      :class="{ active: ind == page }"
      @click="getData(ind)"
    >
      {{ ind }}
    </button>
    <button :disabled="page == totalPage / limit" @click="getData('next')">
      Next
    </button>
    <pre>
      {{ dataMasterLoop }}
    </pre>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "HomeView",
  mounted() {
    this.totalPage = this.dataMaster.length;
    this.getData();
  },
  methods: {
    getData(type = null) {
      if (type == "next") {
        this.page++;
      } else if (type == "prev") {
        this.page--;
      } else {
        this.page = 1;
      }
      if (typeof type == "number") {
        this.page = type;
      }
      const hasil = this.page * this.limit - this.limit;
      this.dataMasterLoop = [];
      this.dataMaster.map((item, index) => {
        if (index >= hasil && this.counLimit < this.limit) {
          // if (this.counLimit != this.limit) {
          this.dataMasterLoop.push(item);
          // }
          this.counLimit++;
        }
      });
      this.counLimit = 0;
    },
  },
  data() {
    return {
      dataMasterLoop: [],
      limit: 2,
      page: 1,
      totalPage: null,
      counLimit: 0,
      dataMaster: [
        {
          id: 1,
          name: 1,
        },
        {
          id: 2,
          name: 2,
        },
        {
          id: 3,
          name: 3,
        },
        {
          id: 4,
          name: 4,
        },
        {
          id: 5,
          name: 5,
        },
        {
          id: 6,
          name: 6,
        },
        {
          id: 7,
          name: 7,
        },
        {
          id: 8,
          name: 8,
        },
        {
          id: 9,
          name: 9,
        },
        {
          id: 10,
          name: 10,
        },
      ],
    };
  },
  components: {
    // HelloWorld,
  },
};
</script>
<style>
.active {
  transform: scale(1.5);
}
</style>
