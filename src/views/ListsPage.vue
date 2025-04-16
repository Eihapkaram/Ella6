<template>
  <div>
    <h3 v-if="this.list.length == 0">list is empty</h3>
    <v-row justify="center" id="con0b">
      <v-table
        style="position: relative"
        id="itemCartcon"
        height="fit-content"
        fixed-header="true"
      >
        <thead class="bg-black">
          <th style="border: 2px solid black">product</th>
          <v-spacer></v-spacer>
          <th width="100px">price</th>
        </thead>
        <br />
        <tr v-for="item in this.list" :key="item.id" class="tr">
          <td>
            <v-row justify="start">
              <v-divider></v-divider>
              <br />
              <v-col
                style="display: flex; flex-flow: column; align-items: center"
                cols="12"
                lg="4"
                md="4"
                sm="4"
              >
                <img
                  id="img"
                  height="100px"
                  width="100px"
                  :src="item.thumbnail"
                />

                <h3>{{ Math.ceil(item.price) }}$</h3>
                <v-col
                  id="detilse"
                  cols="12"
                  lg="7"
                  md="7"
                  sm="5"
                  style=""
                  align-self="center"
                >
                  <span class="text-h6">{{ item.title.slice(0, 15) }} ...</span>
                </v-col>
              </v-col>
            </v-row>
          </td>

          <br />
          <td class="" id="btns" style="">
            <v-row style="flex-flow: row; gap: 10px; position: relative">
              <v-col style="padding: 0px"
                ><v-btn @click="this.delitemL(item.id)">remove</v-btn></v-col
              >
              <v-col style="padding: 0px">
                <v-btn
                  @click="
                    $router.push({
                      name: 'derilse',
                      params: { idparam: item.id },
                    })
                  "
                  >detiles</v-btn
                ></v-col
              >
            </v-row>
          </td>
        </tr>
      </v-table>
    </v-row>
  </div>
</template>
<script>
import { ListsStore1 } from "@/store/Lists";
import { mapActions, mapState } from "pinia";
export default {
  data() {
    return {
      shipping: 20,
      item: "",
      nums: [],
      total: [],
      itemurl: ["home", "cartpage", "checkout"],
      cantry: ["Egypt", "afercan", "alex"],
      email: "",
      select: "",
      checkbox: "",
    };
  },
  computed: { ...mapState(ListsStore1, ["list"]) },
  methods: {
    ...mapActions(ListsStore1, ["GetCartL", "delitemL", "updateL"]),
    muns(item) {
      let q = item.quantity;
      if (q == 1) {
        return;
      } else {
        item.quantity--;
      }
    },
  },

  async mounted() {
    window.scroll(0, 0);
    await this.GetCartL();
  },
};
</script>
<style lang="css" scoped>
#btns {
  flex-flow: row, nowrap;
  justify-content: center;
  align-items: center;
  top: 30px;
  position: relative;
}
#itemCartcon {
  width: 100%;
}
#con0b {
  width: 100%;
  position: relative;
  top: -240px;
}
#detilse {
  position: relative;
  height: 100%;
}
#bgtr {
  width: 100%;
}
/*/desktop/*/
@media (max-width: 1366px) {
}
/*/tablet/*/
@media (max-width: 991px) {
  #con0b {
    width: 98%;
    left: 20px;
    position: relative;
    top: -300px;
  }
  #btns {
    position: relative;
    flex-flow: row, nowrap;
    justify-content: center;
    align-items: center;
    top: 30px;
  }
}
/*/mobile/*/
@media (max-width: 500px) {
  #btns {
    flex-flow: column, nowrap;
    display: flex;
    justify-content: center;
    align-items: center;
    left: 10px;
    top: 80px;
    position: relative;
  }
  #con0b {
    width: 100%;
    top: -300px;
    display: flex;
    align-content: center;
    flex-flow: row;
  }
  #detilse {
    position: relative;
    left: 5px;
    height: 100%;
    display: flex;
    margin-left: 0px;
  }
  #img {
    position: relative;
    left: px;
  }
}
</style>
