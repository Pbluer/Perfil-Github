<template>
  <v-container>
    <v-row class="mt-5">
      <v-card  height="65vh" class="mr-9 rounded-xl">
        <div class="d-flex justify-center">
          <v-img
            class="m-0 rounded-xl"
            width="20vw"
            :src="profile.avatar_url"
          ></v-img>
        </div>
        <v-container class="d-flex flex-row align-center mb-0">
          <h1>{{ profile.name }}</h1>
          <p style="margin: 0 0 0 20px">Nick: {{ profile.login }}</p>
        </v-container>
        <v-container class="d-flex flex-row justify-center mt-0">
          <h4>Seguidores: {{ profile.followers }}</h4>
          <h4 class="ml-5"><v-icon color="red">fa-star</v-icon> {{ star }}</h4>
        </v-container>
      </v-card>

      <v-card>
        <v-simple-table height="65vh">
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">Nome</th>

              <th class="text-left">Linguagem</th>
              <th class="text-left">
                <v-icon color="red">fa-star</v-icon>
              </th>
              <th class="text-left">
                <v-icon color="red">fa-eye</v-icon>
              </th>
              <th class="text-left">
                <v-icon color="red">Link</v-icon>
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in repor" :key="item.nome">
              <td>{{ item.name }}</td>
              <td>{{ item.language }}</td>
              <td>{{ item.stargazers_count }}</td>
              <td>{{ item.watchers_count }}</td>
              <v-btn :href="item.html_url"> <v-icon color="black">fa-link</v-icon> </v-btn>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
      </v-card>

      <v-spacer></v-spacer>
    </v-row>
  </v-container>
</template>

<script>
import Axios from "axios";

export default {
  async created() {
    this.profile = await this.getProfile("");
    this.star = await this.getAllStar();
    this.repor = await this.getAllRepor();
  },
  data: () => ({
    profile: [],
    profileSelected: "Pbluer",
    star: 0,
    repor: [],
  }),
  methods: {
    async getProfile() {
      const { data } = await Axios.get(
        "https://api.github.com/users/" + this.profileSelected
      );
      return data;
    },
    async getAllStar() {
      let star = 0;
      const { data } = await Axios.get(
        "https://api.github.com/users/" + this.profileSelected + "/starred"
      );
      data.forEach(() => star++);
      return star - 1;
    },
    async getAllRepor() {
      const { data } = await Axios.get(
        "https://api.github.com/users/" + this.profileSelected + "/repos"
      );
      return data;
    },
  },
};
</script>
