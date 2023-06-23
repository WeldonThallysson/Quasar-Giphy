<template>
  <header class="bg-dark header row">
    <q-img :src="logo" style="height: 120px; max-width: 150px" />

    <div class="Div_Search">
      <q-input
        class="Input_Search"
        rounded
        filled
        v-model="text"
        color="dark-gray"
        label="Search Giphy"
        label-color="dark-gray"
        bg-color="white"
      />

      <q-btn
        class="button"
        flat
        style="color: white"
        label="Search Giphy"
        @click="
          () => {
            getGiphys();
          }
        "
      />
    </div>
  </header>
  <main>
    <q-parallax
      class="Parallax__Image"
      height="760"
      src="../../assets/giphyseriesc.gif"
    >
    </q-parallax>

    <div class="q-pa-md">
      <q-infinite-scroll class="List_Items">
        <div v-for="dado of dados" :key="dado.id" class="caption">
          <ul>
            <li class="Items_Giphy">
              <p class="Subtitle_Giphy text-black">{{ dado.title }}</p>
              <iframe
                :src="dado.embed_url"
                frameBorder="0"
                class="giphys iframe_Item"
                allowFullScreen
              ></iframe>

              <p class="Subtitle_Giphy">
                <a
                  href="https://giphy.com/gifs/pop-bubble-blowing-63QRL8jwzdrZk66lBf"
                  >via GIPHY</a
                >
              </p>
            </li>
          </ul>
        </div>
      </q-infinite-scroll>
    </div>
  </main>
</template>
<script>
import { defineComponent, ref } from "vue";
import { api } from "../../boot/axios";
import API_KEY from "../../boot/API_KEY";
import logo from "../../assets/logo.png";

export default defineComponent({
  name: "headerSearch",
  components: {},

  data() {
    return {
      dados: [],

      page: 1,
    };
  },

  mounted() {
    this.getAll();
  },
  setup() {
    const text = ref("");

    async function getGiphys() {
      try {
        const response = await api.get("v1/gifs/search", {
          params: {
            api_key: API_KEY,
            q: this.text,

            lang: "pt",
          },
        });
        this.dados = response.data.data;
      } catch (err) {
        console.log(err);
      }
    }

    async function getAll() {
      try {
        const response = await api.get("v1/gifs/search", {
          params: {
            api_key: API_KEY,
            q: "meme",
            lang: "pt",
          },
        });
        this.dados = response.data.data;
      } catch (err) {
        console.log(err);
      }
    }

    return {
      text: ref(""),
      getGiphys,
      getAll,

      logo,
    };
  },
});
</script>
<style scoped="css" src="./style.css" />
